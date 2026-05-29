# Work Vault

Personal work knowledge base — meeting notes, API references, refactor proposals, and technical documentation for the Sonic Equipment stack.

## Structure

```
Work/
├── docs/
│   ├── sonic-equipment-web.md          — Next.js storefront architecture, routes, env vars
│   ├── sentry-noise-inventory.md        — CS-facing cheat sheet for known browser/extension issues
│   ├── storefront api docs/             — Storefront API V1 reference (one file per service group)
│   └── cache invalidation service/      — Sonic.ControlPanel.Api cache flush/invalidation endpoints
├── notes/
│   ├── Email Assistant/                 — daily digests, follow-ups, sender context, coworker notes
│   └── Update SonicEquipmentUI npm token.md
└── refactor/                            — code improvement proposals and tech debt tracking
```

## Key docs

| Doc | What it covers |
|-----|---------------|
| [sonic-equipment-web](docs/sonic-equipment-web.md) | Storefront architecture, middleware pipeline, env vars |
| [Storefront API V1](docs/storefront%20api%20docs/Storefront%20api.md) | Host, auth, service map |
| [Service Relations](docs/storefront%20api%20docs/RELATIONS.md) | How API service groups relate to each other |
| [Cache Invalidation Service](docs/Cashe%20invalidation%20service.md) | Flush/invalidate cache endpoints |
| [Customer Support — Known Browser Issues](docs/Customer%20Support%20%E2%80%94%20Known%20Browser%20Issues.md) | CS paste-ready replies for 4 known browser/extension cases |

## Refactor proposals

- [Spider Pattern CI Check](refactor/Spider%20Pattern%20CI%20Check.md) — GitHub Action enforcing spider module pattern on PRs
- [UI lib data fetching separation](refactor/UI%20lib%20data%20fetching%20separation.md) — move React Query to consuming apps; injectable fetch adapter
- [Remove Pages from UI Lib](refactor/Remove%20Pages%20from%20UI%20Lib.md) — remove all `src/pages/` exports; major version bump
