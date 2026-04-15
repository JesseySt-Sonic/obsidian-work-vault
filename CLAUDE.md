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
│   ├── storefront api docs/   ← Storefront API V1 reference docs
│   │   ├── index.md           ← service map and auth info
│   │   ├── RELATIONS.md       ← relationships between services
│   │   └── *.md               ← one file per service group
│   └── cache invalidation service/
│       └── index.md           ← Sonic.ControlPanel.Api, cache flush/invalidation endpoints
├── notes/
│   └── Update SonicEquipmentUI npm token.md   ← steps to rotate the npm publish token in Azure DevOps
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

- [Storefront API V1](docs/storefront%20api%20docs/index.md) — host, auth, service map
- [Service Relations](docs/storefront%20api%20docs/RELATIONS.md) — how services relate to each other
- [Cache Invalidation Service](docs/cache%20invalidation%20service/index.md) — Sonic.ControlPanel.Api, flush/invalidate cache endpoints
