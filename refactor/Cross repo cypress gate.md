# Cross-Repo Cypress Gate — Refactor Plan

## Goal

Block PRs in [[sonic-equipment-web]] that promote changes to `production` until the full Cypress suite from [[test-automation]] passes against the PR's Vercel preview deployment.
No green check, no merge — enforced at the branch protection level, not by convention.

---

## The Cross-Repo Rules

The Cypress suite lives in `test-automation` and must stay there — it's shared tooling, not app code. But the gate runs on PRs in `sonic-equipment-web`. Two repos, one required check.

1. **Single source of truth for tests** — the suite is defined once in `test-automation` and consumed by any repo that needs it.
2. **Tests run against the real preview** — Cypress hits the Vercel preview URL for the PR, not localhost, not staging.
3. **Required check on `production`** — branch protection blocks merge until the cross-repo job reports success.

```
sonic-equipment-web (PR → production)
        │
        ├── waits for Vercel preview
        │
        └── calls reusable workflow ──► test-automation/cypress-suite.yml
                                              │
                                              └── runs against preview URL
```

See GitHub's docs on [reusing workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows) for the underlying mechanism.

---

## Implementation

### Step 1 — Reusable Workflow in `test-automation`

**File:** `test-automation/.github/workflows/cypress-suite.yml`

A `workflow_call`-triggered workflow that accepts a target URL and runs the full Cypress suite against it. Lives in `test-automation` so the suite stays owned by the QA tooling, not by the app repo.

```yaml
name: Cypress Suite
on:
  workflow_call:
    inputs:
      target-url:
        required: true
        type: string
      commit-sha:
        required: false
        type: string
        description: SHA to report status against (optional, for traceability)

jobs:
  cypress:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: pnpm/action-setup@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 22
          cache: pnpm
      - run: pnpm install --frozen-lockfile
      - uses: cypress-io/github-action@v6
        with:
          install: false
          config: baseUrl=${{ inputs.target-url }}
          browser: chrome
```

**Repo access setting** — in `test-automation` → Settings → Actions → General → "Access", set to **"Accessible from repositories in the 'Sonic-Equipment' organization"**. Without this, the call from `sonic-equipment-web` fails with a 404.

### Step 2 — Caller Workflow in `sonic-equipment-web`

**File:** `sonic-equipment-web/.github/workflows/pr-to-production.yml`

Runs on every PR targeting `production`. Two jobs: wait for the Vercel preview, then call the reusable workflow with the preview URL.

```yaml
name: PR to Production
on:
  pull_request:
    branches: [production]

jobs:
  wait-for-preview:
    runs-on: ubuntu-latest
    outputs:
      preview-url: ${{ steps.preview.outputs.url }}
    steps:
      - name: Wait for Vercel preview
        id: preview
        uses: patrickedqvist/wait-for-vercel-preview@v1.3.2
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          max_timeout: 600

  e2e:
    needs: wait-for-preview
    uses: Sonic-Equipment/test-automation/.github/workflows/cypress-suite.yml@main
    with:
      target-url: ${{ needs.wait-for-preview.outputs.preview-url }}
      commit-sha: ${{ github.event.pull_request.head.sha }}
    secrets: inherit
```

`secrets: inherit` passes any repo/org secrets the Cypress suite needs (Cypress Cloud record key, test credentials) without re-declaring them.

### Step 3 — Branch Protection on `production`

In `sonic-equipment-web` → Settings → Branches → `production` rule:

- Require status checks to pass before merging: **enabled**
- Required check: **`e2e / cypress`** (the job name from the reusable workflow, prefixed with the caller job name)
- Require branches to be up to date before merging: **enabled** (otherwise the preview might lag behind `production`)

The exact required-check name only appears in the dropdown after the workflow has run at least once on a PR — so open a throwaway PR first to register the check, then configure protection.

---

## Workflow Output (success case)

```
✅ wait-for-preview — preview ready at https://sonic-equipment-web-git-feat-checkout-sonic-equipment.vercel.app (2m 14s)
✅ e2e / cypress     — 47 tests passed, 0 failed (8m 32s)

All checks passed. Ready to merge.
```

## Workflow Output (failure case)

```
✅ wait-for-preview — preview ready at https://sonic-equipment-web-git-feat-checkout-sonic-equipment.vercel.app (2m 14s)
❌ e2e / cypress     — 45 passed, 2 failed (7m 51s)
   ✗ checkout.cy.ts — "applies discount code"
   ✗ checkout.cy.ts — "shows tax breakdown on PDP price"

Merge blocked by branch protection. See Cypress Cloud run for full trace.
```

---

## Out of Scope

- **Unit tests, type checks, lint** — assumed already wired up in `sonic-equipment-web` as separate required checks; this plan only adds the E2E gate
- **PRs targeting `develop`** — keep current setup, this only fires on PRs to `production`
- **Visual regression tests** — defer; add as a second job in `cypress-suite.yml` once the basic gate is stable
- **`repository_dispatch` + polling** — rejected as an alternative; reusable workflows give native required-check integration without PAT management
- **Self-hosted runners** — defer unless the suite gets too slow on `ubuntu-latest`

---

## Rollout

| Step | Action | Effort |
|---|---|---|
| 1 | Add `cypress-suite.yml` to `test-automation`, set org access | ~45 min |
| 2 | Add `pr-to-production.yml` to `sonic-equipment-web` | ~30 min |
| 3 | Open throwaway PR to `production` — confirm both jobs run, capture the check name | 15 min |
| 4 | Enable branch protection rule with `e2e / cypress` as required check | 10 min |
| 5 | Verify a failing test actually blocks merge (intentionally break a test in a PR) | 15 min |

Start with steps 1–2 in parallel; the throwaway PR in step 3 is the integration test for the whole pipeline.

---

## Gotchas

- **Workflow file must exist on the default branch of `test-automation`** before `@main` references resolve. Merge the reusable workflow first, then reference it.
- **`secrets: inherit` doesn't cross orgs** — fine here since both repos are under `Sonic-Equipment`, but worth noting if `test-automation` ever moves.
- **Vercel preview URL format can change** — the `wait-for-vercel-preview` action reads the URL from Vercel's deployment status, not by constructing it. Don't hardcode the URL pattern.
- **Required check naming** — the check appears as `<caller-job-name> / <reusable-job-name>`, i.e. `e2e / cypress`. If you rename either job, the required-check entry in branch protection silently stops matching and the gate effectively disables itself. Add a note to the team runbook.
