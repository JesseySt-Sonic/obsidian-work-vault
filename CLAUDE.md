# Claude Instructions — Work Vault

This is Jesse's personal work vault, managed in Obsidian. You have filesystem access via MCP.

## What this vault is for

- **Note taking** — meeting notes, decisions, observations
- **Docs** — Jesse's own reference documentation for APIs and apps
- **Refactor ideas** — code improvement proposals and tech debt tracking

## Vault structure

```
Work/
├── INDEX.md          ← vault home (also symlinked as README.md for GitHub)
├── CLAUDE.md         ← this file
├── docs/
│   ├── sonic-equipment-web.md ← Next.js storefront design document (architecture, routes, env vars)
│   ├── sentry-noise-inventory.md ← CS-facing cheat sheet for known browser/extension issues (paste-ready replies; tech detail in SD-623)
│   ├── storefront api docs/   ← Storefront API V1 reference docs
│   │   ├── index.md           ← service map and auth info
│   │   ├── RELATIONS.md       ← relationships between services
│   │   └── *.md               ← one file per service group
│   └── cache invalidation service/
│       └── index.md           ← Sonic.ControlPanel.Api, cache flush/invalidation endpoints
├── notes/
│   ├── Update SonicEquipmentUI npm token.md   ← steps to rotate the npm publish token in Azure DevOps
│   └── Email Assistant/                        ← email assistant memory + daily digests
│       ├── context.md                          ← sender rules, folder structure, coworker tracking config
│       ├── follow-ups.md                       ← pending follow-up tracker
│       ├── yyyy-mm-dd.md                       ← one digest per run (e.g. 2026-04-28.md)
│       ├── weekly/                             ← weekly digests (one per week, e.g. 2026-W18.md)
│       └── coworkers/                          ← one note per tracked sender
└── refactor/         ← created as refactor ideas are added
```

## How to work with this vault

- **Reading**: prefer reading `index.md` files first to orient before diving into specific files
- **Writing**: match the existing markdown style — keep it concise and reference-oriented, not prose-heavy
- **Links**: this is an Obsidian vault — internal links use `[[wiki-link]]` syntax
- **`.base` files**: Obsidian Bases (structured tables) — treat as read-only unless Jesse asks you to edit them
- **When adding API docs**: always ask Jesse for the base URL of the service across all relevant environments (e.g. local, dev, staging, production) before writing the doc — the host section should cover every env
- **Don't create new folders** without checking with Jesse first
- **Keep CLAUDE.md in sync**: after any change to the vault (new files, new folders, restructuring), update this file to reflect the new state — structure tree, key docs list, or any relevant notes

## Key docs

- [sonic-equipment-web](docs/sonic-equipment-web.md) — Next.js storefront: architecture, routes, middleware pipeline, env vars
- [Customer Support — Known Browser Issues](Customer%20Support%20—%20Known%20Browser%20Issues.md) — CS-facing cheat sheet (4 cases, paste-ready replies). Tech detail lives in [SD-623](https://sonic-equipment.atlassian.net/browse/SD-623).
- [Storefront API V1](Storefront%20api.md) — host, auth, service map
- [Service Relations](docs/storefront%20api%20docs/RELATIONS.md) — how services relate to each other
- [Cache Invalidation Service](Cashe%20invalidation%20service.md) — Sonic.ControlPanel.Api, flush/invalidate cache endpoints

## Refactor plans

- [Spider Pattern CI Check](refactor/Spider%20Pattern%20CI%20Check.md) — GitHub Action to enforce spider module pattern on PRs to develop
- [UI lib data fetching separation](refactor/UI%20lib%20data%20fetching%20separation.md) — move data fetching/React Query to the consuming app; make `request.ts` use an injectable fetch adapter so Next.js cache logic isn't scattered in service files
- [Remove Pages from UI Lib](refactor/Remove%20Pages%20from%20UI%20Lib.md) — remove all `src/pages/` exports (page assemblies + connected components); relocate pure UI to new `src/checkout/`, `src/my-sonic/`, `src/product/` dirs; major version bump
