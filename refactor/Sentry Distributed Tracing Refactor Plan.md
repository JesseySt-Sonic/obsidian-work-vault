# Sentry Distributed Tracing — Refactor Plan

## Goal

Connect errors across services so that domino-effect issues are visible in a single trace,
rather than appearing as unrelated errors scattered across the storefront, BFF, Storefront API,
and Cloudflare proxy.

---

## Services in Scope

| Service | Role |
|---|---|
| Cloudflare reverse-proxy | Entry point — all traffic passes through here |
| Next.js storefront | Frontend — what the user sees |
| BFF API | Orchestration layer between frontend and backend |
| Storefront API | Core business logic (products, shipping, checkout) |

---

## Phase 1 — Correlation ID (Quick Win)

**Goal:** Give every request a shared ID that appears in all Sentry events across all services,
so you can search for one ID and see everything that happened in that request.

**Where:** Cloudflare reverse-proxy

**What to do:**

Generate a `x-correlation-id` header on every incoming request if one isn't already present,
and forward it downstream. Every service then reads this header and sets it as a Sentry tag.

```js
// Cloudflare Worker
export default {
  async fetch(request) {
    const correlationId = request.headers.get("x-correlation-id") ?? crypto.randomUUID();
    const newRequest = new Request(request, {
      headers: { ...Object.fromEntries(request.headers), "x-correlation-id": correlationId },
    });
    return fetch(newRequest);
  },
};
```

```js
// Every downstream service (Next.js, BFF, Storefront API)
import * as Sentry from "@sentry/node"; // or @sentry/nextjs

const correlationId = request.headers["x-correlation-id"];

Sentry.configureScope((scope) => {
  scope.setTag("correlation_id", correlationId);
  scope.setTag("service", "bff-api"); // use the correct service name per service
});
```

**Result:** You can search `correlation_id:<value>` in Sentry and instantly see every event
across all 4 services for that single user request.

---

## Phase 2 — Sentry Trace Propagation

**Goal:** Link Sentry events into a single distributed trace with a waterfall view, so you can
see parent/child relationships between service calls.

**Where:** All services — any place that makes an outgoing HTTP request.

**What to do:**

Ensure the `sentry-trace` and `baggage` headers are forwarded on every outgoing fetch or
HTTP call. Sentry's SDK can inject these automatically if configured correctly.

```js
// Any service making outbound HTTP calls
import * as Sentry from "@sentry/node";

const response = await fetch(upstreamUrl, {
  headers: {
    ...existingHeaders,
    ...Sentry.getTraceData(), // injects sentry-trace + baggage
  },
});
```

For Next.js, enable tracing in `sentry.server.config.js`:

```js
import * as Sentry from "@sentry/nextjs";

Sentry.init({
  dsn: process.env.SENTRY_DSN,
  tracesSampleRate: 1.0,
  tracePropagationTargets: [
    "localhost",
    /^https:\/\/your-bff-api\.internal/,
    /^https:\/\/your-storefront-api\.internal/,
  ],
});
```

**Result:** Sentry's Trace Explorer shows a waterfall of every span across all services
for a single request, with the originating event at the top.

---

## Phase 3 — User Error Breadcrumbs

**Goal:** Capture user-caused preconditions (invalid input, bad state) as breadcrumbs so they
appear in the trace before the actual exception, making root cause obvious.

**Where:** Any service that accepts and validates user input — primarily the BFF and Storefront API.

**What to do:**

When user input fails validation or produces a known bad state, add a breadcrumb and optionally
capture a warning-level message rather than silently discarding the error.

```js
// Example: invalid address submitted during checkout
Sentry.addBreadcrumb({
  category: "user.input",
  message: "User submitted address that failed validation",
  level: "warning",
  data: {
    addressId: address.id,
    validationErrors: errors, // e.g. ["postal_code_not_found"]
    userId: session.userId,
  },
});

// Optionally surface as a warning so it's searchable even without a downstream error
Sentry.captureMessage("Invalid address submitted to checkout", "warning");
```

**Result:** When a downstream error occurs (e.g. shipping calculation failure), the breadcrumb
trail will show the invalid address as the root cause, even across service hops.

---

## Phase 4 — Root Cause Tagging on Re-thrown Errors

**Goal:** When a service catches an error and re-throws it, annotate it with context about
what the likely root cause is, so the error in Sentry is self-explanatory.

**Where:** Any service that catches and re-throws errors from upstream calls.

**What to do:**

Wrap caught errors with additional Sentry context before re-throwing:

```js
try {
  await calculateShipping(cart);
} catch (err) {
  Sentry.withScope((scope) => {
    scope.setContext("checkout_state", {
      addressValidated: cart.shippingAddress?.validated ?? false,
      addressId: cart.shippingAddress?.id,
      cartId: cart.id,
    });
    scope.setTag("root_cause_hint", "invalid_address"); // searchable
    Sentry.captureException(err);
  });
  throw err;
}
```

**Result:** Errors in Sentry carry checkout/request state at the time of failure, and can be
filtered by `root_cause_hint` to find patterns across many users.

---

## Rollout Order

| Step | Phase | Effort | Impact |
|---|---|---|---|
| 1 | Phase 1 — Correlation ID | Low — 1 file per service | Immediate: all events linkable by ID |
| 2 | Phase 2 — Trace propagation | Medium — touch every fetch call | High: full waterfall in Trace Explorer |
| 3 | Phase 3 — User breadcrumbs | Low — add to validation logic | High: root cause visible before the error |
| 4 | Phase 4 — Root cause tagging | Low — wrap existing catch blocks | Medium: better signal in Sentry issues |

Start with Phase 1 in the Cloudflare proxy — it's a single deployment with zero risk and
immediately makes all existing errors correlatable.

---

## What You'll See in Sentry After This

For the address → shipping error scenario:

```
Trace: [abc-123] POST /checkout
  ├─ cloudflare          entry                         12ms
  ├─ nextjs              checkout page submit          180ms
  ├─ bff-api             POST /checkout/initiate       160ms
  │    breadcrumb ⚠      user submitted invalid address (postal_code_not_found)
  └─ storefront-api      GET /shipping/calculate       ❌ UnresolvableAddressError
       context:          addressValidated: false
       root_cause_hint:  invalid_address
```

Instead of seeing an opaque `UnresolvableAddressError` with no context, you'll see the
full chain — including the user action that caused it.
