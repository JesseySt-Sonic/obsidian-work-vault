# UI Lib Data Fetching Separation

> **Status:** Lab-time experiment — no current project pressure. Try it out when there's a free lab slot.

When we move to a single consuming Next.js app, the library should be a pure UI lib — components and fetch functions only. Data fetching, cache strategy, and React Query wiring move to the app.

## request.ts — adapted fetch

Rather than scattering `next: { revalidate, tags }` across every function in `bff-service.ts`, `request.ts` should accept an adapted `fetch` implementation injected by the consumer. The app passes a Next.js-aware fetch (or a plain fetch for tests/client), and `request.ts` stays agnostic.

```ts
// app initialises once
import { request } from '@sonic/ui'
request.fetch = fetch // Next.js's extended fetch, already patched globally in App Router
```

`bff-service.ts` keeps passing `next: { tags }` as options — Next.js activates them only when its patched fetch is in use. On the client, a plain fetch silently ignores them.

## React Query

The hooks (`useFetchNavigationLinks` etc.) either:
- Move to the app entirely, or
- Are removed in favour of the prefetch + `HydrationBoundary` pattern (server prefetches via `queryClient.prefetchQuery`, client hydrates from dehydrated state)

This eliminates the current double-cache situation where Next.js Data Cache and React Query cache operate independently with no coordination.

## Tauri / mobile app

Because `next: { tags, revalidate }` are just unknown extra properties on the fetch `init` object, any non-Next.js fetch implementation silently ignores them. `bff-service.ts` needs no changes — adapters decide what to do.

`@tauri-apps/plugin-http` already exposes a fetch-compatible API, so the Tauri adapter is trivial:

```ts
import { fetch as tauriFetch } from '@tauri-apps/plugin-http'
request.fetch = tauriFetch
```

Tauri's HTTP stack routes through the native layer — no CORS restrictions, system proxy support. Caching can be handled independently (e.g. SQLite persister via TanStack Query's persist client).

| Consumer | Adapter | Caching |
|---|---|---|
| Next.js app | global patched `fetch` (App Router) | Next.js Data Cache + React Query hydration |
| Tauri app | `@tauri-apps/plugin-http` | own strategy (SQLite persister etc.) |
| Tests | `msw` / mock fetch | none |

The library has no Next.js imports and makes no runtime assumptions — the only contract is *give me something shaped like `fetch`*.

## Files affected

- `src/shared/fetch/request.ts` — add injectable fetch adapter
- `src/shared/api/bff/services/bff-service.ts` — no structural change needed; `next` options stay but only activate server-side
- `src/shared/api/bff/hooks/use-fetch-navigation-links.ts` (and sibling hooks) — move to app or delete
