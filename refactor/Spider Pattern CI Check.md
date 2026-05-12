# Spider Pattern CI Check — Refactor Plan

## Goal

Automatically enforce the spider module pattern in [[sonic-equipment-web]] on every PR to `develop`.
The check catches import violations before they land in the codebase — no manual review needed.

---

## The Spider Pattern Rules

`core/` is the foundation. All other modules may import from `core/`, but:

1. **`core/` has no outbound deps** — files under `src/modules/core/` must not import from any other `@/modules/` path.
2. **No cross-module imports** — files under any other module (`auth/`, `api/`, `routing/`, etc.) may only import from `@/modules/core/`, never from each other.

```
analytics   api   auth   i18n   proxy   routing
    └──────────────────┬──────────────────┘
                     core
```

See [[src/modules/modules.md]] for the full module reference.

---

## Implementation

### Step 1 — Validation Script

**File:** `scripts/check-spider-pattern.mjs`

A ~30-line Node.js script (no dependencies beyond Node built-ins) that:

1. Globs all `.ts` / `.tsx` files under `src/modules/`
2. For each file, extracts `import` / `require` statements via regex
3. Applies the two rules:
   - Core files: fail if any import matches `@/modules/(?!core/)`
   - Other files: fail if any import matches `@/modules/(?!core/)` (i.e. cross-module)
4. Prints a violation list and exits non-zero if any found

```js
// pseudo-code outline
const files = glob('src/modules/**/*.{ts,tsx}')
for (const file of files) {
  const module = file.split('/')[2]           // e.g. "core", "auth"
  const imports = extractModuleImports(file)  // all @/modules/... imports
  for (const imp of imports) {
    if (module === 'core' && imp !== 'core') violation(file, imp)
    if (module !== 'core' && imp !== 'core') violation(file, imp)
  }
}
```

### Step 2 — GitHub Actions Workflow

**File:** `.github/workflows/spider-pattern.yml`

Runs on every PR targeting `develop`. Fails the PR if any violation is found.

```yaml
name: Spider Pattern Check
on:
  pull_request:
    branches: [develop]
jobs:
  check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: pnpm/action-setup@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 22
          cache: pnpm
      - run: node scripts/check-spider-pattern.mjs
```

No `pnpm install` needed — the script uses only Node built-ins (`fs`, `path`, `glob` via `node:fs`).

---

## Violation Output Format

```
❌ Spider pattern violation in src/modules/auth/session.ts
   imports @/modules/i18n/context — cross-module imports are not allowed
   only @/modules/core/* is permitted

❌ Spider pattern violation in src/modules/core/cookies.ts
   imports @/modules/i18n/types — core/ must have no outbound module dependencies

2 violations found. See src/modules/modules.md for the spider pattern rules.
```

---

## Out of Scope

- **Intra-module imports** (e.g. `auth/` importing its own `./utils`) — always fine, not checked
- **Non-module paths** (`@/app/`, `@/components/`, third-party packages) — not checked
- **`eslint-plugin-boundaries`** — a heavier alternative if ESLint rules are needed in-editor too; defer unless violations start slipping through locally

---

## Rollout

| Step | Action | Effort |
|---|---|---|
| 1 | Write `scripts/check-spider-pattern.mjs` | ~1h |
| 2 | Add `.github/workflows/spider-pattern.yml` | 15 min |
| 3 | Verify locally (`node scripts/check-spider-pattern.mjs`) | 15 min |
| 4 | Open PR to `develop` — confirm workflow runs green | — |

Start with step 1 and test locally before wiring up the action.
