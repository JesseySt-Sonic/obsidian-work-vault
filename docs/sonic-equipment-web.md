---
title: sonic-equipment-web — Design Document
updated: 2026-04-16
---

# sonic-equipment-web

B2B e-commerce storefront for Sonic Equipment. A Next.js 15 App Router application with multi-locale support, Storyblok CMS integration, Algolia search, and an ASP.NET-compatible backend session model.

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Next.js 15 (App Router), React 19 |
| Language | TypeScript 5 |
| Package manager | pnpm |
| UI library | `@sonic-equipment/ui` (internal, versioned) |
| CMS | Storyblok |
| Search | Algolia |
| Server state | TanStack React Query 5 |
| Error tracking | Sentry |
| Analytics | Google Analytics / Google Tag Manager |
| Payments | Adyen |
| Cookie consent | Cookiebot |
| Deployment | Vercel |

---

## Route Map

All routes are scoped under the `[languageCountryCode]` segment (e.g. `/en-nl/products`).

### Public

| Path | Purpose |
|---|---|
| `/products/[[...slugs]]` | Product listing (PLP) or product details (PDP) — resolved by slug |
| `/story/[[...slugs]]` | CMS-driven content pages (Storyblok) |
| `/search` | Global search results |
| `/cart` | Shopping cart |
| `/signin` | Authentication |
| `/create-account` | Registration |
| `/change-password` | Password reset |
| `/countries` | Country / locale selector |

### Authenticated (`/my-sonic/`)

| Path | Purpose |
|---|---|
| `/my-sonic/account` | Account settings (default `/my-sonic` rewrite) |
| `/my-sonic/orders` | Order history |
| `/my-sonic/orders/[id]` | Order detail |
| `/my-sonic/favorites` | Saved items |
| `/my-sonic/addresses/bill-to/[billToId]/ship-to/[shipToId]` | Address management |
| `/my-sonic/upload-order` | CSV bulk order upload |

### Checkout

| Path | Purpose |
|---|---|
| `/checkoutshipping` | Shipping address |
| `/checkoutreviewandsubmit` | Review & place order |
| `/orderconfirmation` | Post-order confirmation |

### Infrastructure

| Path | Purpose |
|---|---|
| `/api/[...path]` | Universal API proxy (BFF + Shop) |
| `/api/revalidate/*` | ISR webhooks (Storyblok, categories, products, translations) |
| `/robots.ts`, `/sitemap.xml` | SEO |

### Legacy redirects (permanent)

Old ASP.NET-era URLs are 301-redirected to their new equivalents (e.g. `/MyAccount/Orders/*` → `/my-sonic/orders/*`). See `next.config.ts`.

---

## Architecture

### Middleware pipeline

Every request (excluding `/api`, static assets, and well-known paths) passes through a sequential chain in `src/middleware.ts`:

```
handle404Rewrites
  → handleOptionsRequests
  → lowerCaseRoutes
  → ensureLocalePrefix         # adds /[languageCountryCode] if missing
  → syncSessionLanguage         # aligns session language with URL locale
  → createCookies               # sets tracking/analytics cookies
  → createHttpHeaders           # sets security headers
  → router                      # routes to Storyblok if valid CMS slug
  → rewriteStoryblokPreview     # rewrites Storyblok preview requests
```

The chain uses a `processMiddleware` utility that short-circuits when a step returns a terminal response. Custom headers injected here (`x-sonic-href`, `x-sonic-language-country-code`, etc.) are consumed downstream in `src/modules/request/request.ts`.

Middleware runs in preferred Vercel regions: `cdg1` (Paris), `fra1` (Frankfurt), `hkg1` (Hong Kong).

### API proxy

All browser-facing API calls go through `/api/[...path]`, which forwards to one of two origin services:

- `/api/v1/bff/*` → `BFF_ORIGIN_API_URL` — Backend For Frontend (auth, account, orders)
- everything else → `SHOP_ORIGIN_API_URL` — Shop/product API

`src/modules/proxy/proxy.ts` handles:
- Header forwarding (strips cookies, reconstructs them)
- SameSite=None enforcement on response cookies
- Cookie domain rewriting via `COOKIE_DOMAIN` env var
- Locale cookie injection (`CurrentLanguageId`, `CurrentCountryId`, `CurrentCurrencyId`, `SetContextLanguageCode`)

### Products page (PDP / PLP)

`src/app/[languageCountryCode]/products/[[...slugs]]/page.tsx` uses a **try-PDP-first, fall-back-to-PLP** pattern:

1. Attempt `fetchProductDetailsPageData` by slug → renders `<SonicUiProductDetails>`
2. If `NotFoundRequestError` → attempt `fetchProductListingPageData` → renders `<ProductListing>`
3. If still `NotFoundRequestError` → `notFound()`

Both page types sharing a single clean URL path (`/products/...`) is intentional — it avoids a `/p/` or `/c/` prefix that would differ from the legacy URLs and is better for SEO continuity. PDP fetch is wrapped in React's `cache()` to deduplicate between the page render and `generateMetadata`. Price data is fetched separately and merged client-side.

### Locale resolution

Locale is a `languageCountryCode` (e.g. `en-nl`) resolved in priority order:

1. URL path segment (`/en-nl/...`)
2. Cookies (`CurrentCountryId` + `CurrentLanguageId`)
3. Accept-Language header (country-code match)
4. Default: `en-nl`

41 supported locales are defined in `locales.json` with `countryId`, `languageId`, `currencyCode`, `languageCultureCode`, etc.

### Caching strategy

| Layer | Mechanism | Scope |
|---|---|---|
| React `cache()` | Request-level deduplication | PDP fetch, shared across page + metadata render |
| Next.js ISR | On-demand revalidation via webhooks | CMS pages, product listings, categories |
| TanStack React Query | Server + client state | Authenticated data (orders, account, cart) |
| Build-time crawl | `pnpm crawl-routes` | Warm ISR cache on deploy |
| Storyblok tags | `['story', 'story-{slug}', ...]` | Fine-grained CMS invalidation |

### Authentication

- Session cookie: `.AspNet.ApplicationCookie` (set by ASP.NET backend, proxied through)
- `verifyAuth()` — server-side utility that redirects unauthenticated users to `/signin?returnUrl=...`
- `allowGuest` flag controls whether unauthenticated access is permitted on a given page

### CMS (Storyblok)

The `router` middleware step checks `isValidStorybookPath()` to decide whether to route a URL to the Storyblok story handler (`/story/[[...slugs]]`). Content components: `CategoryList`, `HomePage`, `LandingPage`, `NewsOverview`.

Preview mode is toggled via `STORYBLOK_IS_PREVIEW` env var and handled by `rewriteStoryblokPreview`.

---

## Key Providers (root layout)

Wrapping order in `[languageCountryCode]/layout.tsx`:

```
ErrorBoundary
  CookieProvider
  ReactQueryContainer
  LocalStorageProvider
  CountryLanguageInformationProvider
  GlobalStateProvider
  GoogleAnalyticsProvider
  ClientIntlProvider
  AlgoliaInsightsProvider
  ToastProvider
  FavoriteProvider
  GlobalSearchProvider
  RouteProvider
  StoryblokProvider
  SidebarProvider
  Cookiebot / GoogleTagManager
```

---

## Environment Variables

| Variable | Purpose |
|---|---|
| `BFF_ORIGIN_API_URL` | BFF service origin (server-side proxy target) |
| `SHOP_ORIGIN_API_URL` | Shop/product API origin (server-side proxy target) |
| `BFF_API_URL` | BFF URL exposed to browser |
| `SHOP_API_URL` | Shop API URL exposed to browser |
| `PROXY_API_URL` | Base URL used for proxy path matching |
| `ALGOLIA_APP_ID` / `ALGOLIA_API_KEY` / `ALGOLIA_HOST` / `ALGOLIA_PROTOCOL` | Search |
| `STORYBLOK_API_TOKEN` | CMS read token |
| `STORYBLOK_IS_PREVIEW` | Enable CMS preview mode |
| `COOKIE_DOMAIN` | Domain applied to proxied set-cookie headers |
| `GTM_ID` | Google Tag Manager container ID |
| `COOKIEBOT_ID` | Cookiebot domain group ID |
| `BASE_URL` | Public base URL for the site |
| `ROBOTS_CAN_INDEX` | Set to `true` on production to allow crawling |
| `MARKETING_HOMEPAGE` | URL of external marketing homepage |

Vercel build info (`VERCEL_GIT_COMMIT_SHA`, `VERCEL_GIT_COMMIT_REF`, `VERCEL_ENV`) is surfaced as `NEXT_PUBLIC_*` env vars for client-side version info.

---

## Build & Scripts

| Script | Purpose |
|---|---|
| `pnpm dev` | Local dev server |
| `pnpm dev:https` | Local dev with HTTPS (required for checkout / Adyen) |
| `pnpm build` | Production build |
| `pnpm build:ci` | sync-locales → crawl-routes → build |
| `pnpm sync-locales` | Pull locale config from backend |
| `pnpm crawl-routes` | Pre-warm ISR cache at deploy time |
| `pnpm test:all` | TSC + ESLint + Stylelint |
| `pnpm storyblok-*` | CMS content sync utilities |

---

## Deployment

- Hosted on **Vercel**
- Sentry source maps uploaded on CI builds (`silent: !process.env.CI`)
- Cron monitors via Sentry + Vercel Cron integration
- Bundle analysis available via `ANALYZE=true pnpm build`

---

## Suggested Improvements

### Should do

#### Formalise the BFF proxy contract

The proxy path matching in `proxy.ts` is an implicit string-based convention (`pathname.includes('/bff')`). Adding a new backend service requires knowing this convention exists.

**Proposal:** Define the target routing in a small config object (e.g. `{ prefix: '/api/v1/bff', target: BFF_ORIGIN_API_URL }`) and loop over it in `mapTargetUrl`. Makes it easy to add services and obvious what routes map where.

---

#### Type the proxy API surface

The proxy currently accepts any path under `/api/[...path]` and routes based on a string prefix. There is no type-level contract between what the frontend calls and what the proxy expects.

**Proposal:** Define a typed API client module (even a thin wrapper over `fetch`) with explicit method signatures per service group. This gives autocomplete, catches typos at compile time, and documents the available API surface in one place rather than scattering bare `fetch` calls across pages.

---

#### Formalise locale fallback behaviour

`getCountryLanguageInformationFromAcceptHeader` matches incoming language codes against `countryCode` in the locale list (e.g. `nl` → NL). This means a browser sending `nl` (Dutch language) matches the Netherlands locale, which may be wrong for a user in Belgium. The fallback is silently swallowed and defaults to `en-nl`.

**Proposal:** Log a structured warning (via the existing `logger`) when the Accept-Language fallback is used so it is visible in Sentry. Separately, evaluate whether country-IP detection (already available as `cf-ipcountry` in the request) should take precedence over Accept-Language for the initial locale guess.

---

### Nice to have

#### Reduce provider nesting in root layout

The root layout wraps content in ~15 nested context providers. This makes the component tree hard to read and diagnose, and React renders all of them on every navigation.

**Proposal:** Consolidate providers that are purely data-containers with no render logic into a single `<AppProviders>` component. Providers that are genuinely independent (e.g. `Cookiebot`, `GoogleTagManager`) can be moved to leaf positions rather than wrapping the full tree.

---

#### Move checkout routes under a shared segment

`/checkoutshipping` and `/checkoutreviewandsubmit` sit at the root level alongside unrelated pages. This makes it harder to apply shared checkout layout, auth guards, or middleware rules to the checkout flow as a unit.

**Proposal:** Move to `/checkout/shipping` and `/checkout/review` under a shared `/checkout/` segment with its own `layout.tsx`. Enables a dedicated checkout shell (progress indicator, stripped nav) and a single `verifyAuth()` call at the layout level.
