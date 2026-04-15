# Provider Tree Refactor Plan

## Current Tree (Annotated)

```
<ErrorBoundary>                              ← Error handling
  <CookieProvider>                           ← Infrastructure (SSR cookies)
    <ReactQueryContainer>                    ← Infrastructure (data fetching)
      <ClientCookieProvider>                 ← Infrastructure (client cookies) ⚠️ duplicate concern
        <LocalStorageProvider>               ← Infrastructure (storage) ⚠️ see storage refactor
          <Prefetch>                         ← ⚠️ not a provider, data loading side effect
            <CountryLanguageInfoProvider>    ← Internationalisation
              <GlobalStateProvider>          ← UI State ⚠️ too broad
                <GoogleAnalyticsProvider>    ← Analytics ⚠️ should not be a provider
                  <ClientIntlProvider>       ← Internationalisation ⚠️ duplicate concern
                    <AlgoliaInsightsProvider> ← Analytics ⚠️ should not be a provider
                      <ToastProvider>        ← UI State
                        <FavoriteProvider>   ← UI State ⚠️ consider Zustand
                          <GlobalSearchProvider> ← UI State
                            <RouteProvider>  ← Routing
                              <StoryblokProvider> ← External integration
                                <NextErrorBoundary> ← Error handling ⚠️ why two?
                                  <SidebarProvider> ← UI State
                                    ...children
                                  <Cookiebot />     ← Analytics/Tracking
                                  <GoogleTagManager /> ← Analytics ⚠️ should not be a provider
```

---

## Categories

### 🔧 Infrastructure
| Provider | Responsibility |
|---|---|
| `CookieProvider` | SSR-side cookie access |
| `ClientCookieProvider` | Client-side cookie access |
| `LocalStorageProvider` | Storage access |
| `ReactQueryContainer` | Data fetching / caching layer |

**Issue:** Two cookie providers exist for the same conceptual reason — one for SSR, one for client. This is the same problem `LocalStorageProvider` has, and the storage refactor (see `storage-hook-refactor-plan.md`) solves it by moving to adapters. The same pattern applies here: a `cookieStorageAdapter` that handles SSR vs client internally removes the need for both cookie providers entirely.

---

### 🌍 Internationalisation
| Provider | Responsibility |
|---|---|
| `CountryLanguageInformationProvider` | Holds country/language data |
| `ClientIntlProvider` | i18n formatting and translations |

**Issue:** These are sequentially dependent — `ClientIntlProvider` almost certainly consumes data from `CountryLanguageInformationProvider`. They are two providers for one concern and should be merged into a single `InternationalisationProvider`.

---

### 📊 Analytics & Tracking
| Provider | Responsibility |
|---|---|
| `GoogleAnalyticsProvider` | GA initialisation |
| `AlgoliaInsightsProvider` | Algolia click/conversion tracking |
| `GoogleTagManager` | GTM script injection |
| `Cookiebot` | Cookie consent management |

**Issue:** None of these need to be providers. They are side effects — they initialise scripts and listeners, they do not provide context that child components consume. They should be collapsed into a single `<AnalyticsBootstrap />` component that runs `useEffect` hooks internally. This alone removes 3–4 levels from the tree.

---

### 🖥️ UI State
| Provider | Responsibility |
|---|---|
| `GlobalStateProvider` | ⚠️ Unknown — name is too broad |
| `GlobalSearchProvider` | Search open/closed state, query |
| `SidebarProvider` | Sidebar open/closed state |
| `ToastProvider` | Toast notifications |
| `FavoriteProvider` | Favorites list state |

**Issues:**
- `GlobalStateProvider` is a red flag name. It almost certainly grew into a dumping ground over time. Audit what it actually contains and split it into domain-specific providers or Zustand stores.
- `ToastProvider` can likely be replaced entirely by a library like [Sonner](https://sonner.emilkowal.ski/) which does not require a provider.
- `FavoriteProvider` and `GlobalSearchProvider` are good candidates for Zustand stores — they are not tree-scoped concerns, they are app-wide state that any component might access.
- `SidebarProvider` is fine as a provider if it is genuinely scoped to the layout.

---

### 🔗 Routing & External Integrations
| Provider | Responsibility |
|---|---|
| `RouteProvider` | Current route / href context |
| `StoryblokProvider` | Storyblok CMS bridge |

**Issue:** `RouteProvider` may be redundant depending on how much of Next.js's own routing hooks (`useRouter`, `usePathname`) you use. Worth auditing whether it adds anything beyond what Next.js already provides.

---

### 🛡️ Error Handling
| Provider | Responsibility |
|---|---|
| `ErrorBoundary` (outer) | Top-level catch-all |
| `NextErrorBoundary` (inner) | Next.js-specific error handling |

**Issue:** Two error boundaries with no clear documented reason for both. If `NextErrorBoundary` is needed for Next.js-specific recovery, it should be documented. Otherwise collapse into one.

---

### ⚠️ Misplaced Components
| Component | Issue |
|---|---|
| `Prefetch` | Not a provider — it's a data loading side effect. Should be a server component or a `useEffect` in the layout, not a wrapper in the provider tree. |

---

## Proposed Reduced Tree

```
<ErrorBoundary>
  <ReactQueryContainer>
    <InternationalisationProvider>        ← merged CountryLanguage + ClientIntl
      <AnalyticsBootstrap />              ← replaces GA, Algolia, GTM, Cookiebot providers
      <ToastProvider />                   ← or replace with Sonner (no provider needed)
      <RouteProvider>                     ← audit if still needed
        <StoryblokProvider>
          <SidebarProvider>
            <div className="page-layout">
              ...children
            </div>
          </SidebarProvider>
        </StoryblokProvider>
      </RouteProvider>
    </InternationalisationProvider>
  </ReactQueryContainer>
</ErrorBoundary>
```

Storage (cookies, localStorage, sessionStorage) moves entirely to adapters — no providers needed.
Global UI state (favorites, search) moves to Zustand — no providers needed.
`GlobalStateProvider` is audited and either split into named stores or eliminated.

---

## Recommended Order of Attack

1. **Storage refactor** — collapse `CookieProvider`, `ClientCookieProvider`, and `LocalStorageProvider` into adapters (see `storage-hook-refactor-plan.md`)
2. **Analytics** — replace `GoogleAnalyticsProvider`, `AlgoliaInsightsProvider`, `GoogleTagManager` with a single `<AnalyticsBootstrap />` component
3. **i18n** — merge `CountryLanguageInformationProvider` and `ClientIntlProvider`
4. **Audit `GlobalStateProvider`** — split by domain, migrate candidates to Zustand
5. **Evaluate `FavoriteProvider` and `GlobalSearchProvider`** — migrate to Zustand stores
6. **Remove `Prefetch`** as a provider wrapper
7. **Collapse error boundaries** — document or remove the duplication
8. **Evaluate `RouteProvider`** — check if Next.js native hooks make it redundant
