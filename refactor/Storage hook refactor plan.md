# Storage Hook Refactor Plan

## Goal

Refactor `useLocalStorage` into a generic, observer-aware storage hook that supports localStorage, sessionStorage, and cookies behind a unified interface.

---

## 1. Define a `StorageAdapter` Interface

Create a common interface all adapters must implement:

```ts
interface StorageAdapter {
  getItem(key: string): string | null
  setItem(key: string, value: string): void
  removeItem(key: string): void
  subscribe(key: string, callback: (value: string | null) => void): () => void
}
```

The `subscribe` method returns an unsubscribe function, consistent with the React `useEffect` cleanup pattern.

---

## 2. Implement an Observer Registry

Create a shared, storage-agnostic event registry that adapters can use internally:

```ts
// storage-emitter.ts
type Listener = (value: string | null) => void

const listeners = new Map<string, Set<Listener>>()

export function emit(key: string, value: string | null) { ... }
export function subscribe(key: string, cb: Listener): () => void { ... }
```

This is the core of the cross-component sync. Each adapter calls `emit` on write/delete, and `subscribe` is used in the hook's `useEffect`.

---

## 3. Implement the Three Adapters

### `localStorageAdapter`
- `getItem`/`setItem`/`removeItem` delegate to `window.localStorage`
- `subscribe` uses the shared observer registry
- Also listens to the native `window` `"storage"` event to handle cross-tab sync

### `sessionStorageAdapter`
- Same structure as `localStorageAdapter` but delegates to `window.sessionStorage`
- No cross-tab sync needed (sessionStorage is tab-scoped by nature)

### `cookieStorageAdapter`
- `getItem`/`setItem`/`removeItem` use custom cookie read/write logic
- `subscribe` uses the same shared observer registry
- Note: no native browser event exists for cookie changes, so same-page observer is the only sync mechanism

---

## 4. Refactor the Hook

Replace `useLocalStorage` with a generic `useStorage` hook:

```ts
function useStorage<T>(
  key: string,
  adapter: StorageAdapter,
  initialValue?: T,
): [T | undefined, (value: T | undefined) => void]
```

Internally it:
1. Reads initial value from `adapter.getItem(key)` once
2. Holds value in `useState`
3. In `useEffect`, calls `adapter.subscribe(key, ...)` and updates state when notified — this is what enables cross-component sync
4. On `setValue`, calls `adapter.setItem`/`removeItem` and the observer emits to all other subscribers

---

## 5. Expose Convenience Hooks

Keep ergonomic named hooks as thin wrappers:

```ts
const useLocalStorage  = (key, initial) => useStorage(key, localStorageAdapter, initial)
const useSessionStorage = (key, initial) => useStorage(key, sessionStorageAdapter, initial)
const useCookieStorage  = (key, initial) => useStorage(key, cookieStorageAdapter, initial)
```

---

## 6. Update the Provider

The `LocalStorageProvider` can be generalised or retired depending on how adapters are instantiated. If adapters are singletons (i.e. just module-level exports), the provider may no longer be necessary. If you need to inject mock adapters for testing, a generic `StorageProvider` accepting an adapter map would replace the current one.

---

## File Structure

```
storage/
  adapters/
    local-storage-adapter.ts
    session-storage-adapter.ts
    cookie-storage-adapter.ts
  storage-emitter.ts
  storage-adapter.ts        ← interface definition
  use-storage.ts            ← generic hook
  use-local-storage.ts      ← convenience wrapper
  use-session-storage.ts    ← convenience wrapper
  use-cookie-storage.ts     ← convenience wrapper
  storage-context.ts        ← optional, if provider pattern is kept
  storage-provider.tsx      ← optional, if provider pattern is kept
```

---

## Migration Path

1. Implement `StorageAdapter` interface and observer registry
2. Implement `localStorageAdapter` first and validate cross-component sync works
3. Refactor `useLocalStorage` to use `useStorage` under the hood — **no consumer changes needed at this step**
4. Add `sessionStorageAdapter` and `cookieStorageAdapter`
5. Expose `useSessionStorage` and `useCookieStorage`
6. Evaluate whether the provider is still needed and remove or generalise it
