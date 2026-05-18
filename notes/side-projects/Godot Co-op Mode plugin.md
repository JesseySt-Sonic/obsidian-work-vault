A Godot editor plugin that adds a social-awareness layer for teams — start with "who is editing what" presence (Discord/Steam style), then grow into ghost cursors and gamified collaboration cues. Sidesteps the CRDT rabbit hole by treating _awareness_ as a separate concern from _version control_.

## Why this scope works

The hard problem in collaborative editing is co-mutating a shared scene graph. The _easy_ problem — and the one with most of the day-to-day value — is just knowing **who is touching what right now**. Figma, VS Code Live Share, and Google Docs all split these architecturally:

- **Awareness layer:** ephemeral, lossy, cheap. Cursors, selections, "who is here."
- **Document layer:** durable, consistent, expensive. The actual CRDT/OT sync.

You can ship the first without the second. Git remains the source of truth for canonical state; the plugin just makes humans aware of each other before they collide.

## Why Godot specifically

- `.tscn` / `.tres` are text and merge cleanly in git — the VCS half is already solved.
- `EditorPlugin` exposes resource open/close signals, so presence hooks are trivial.
- The scene tree is a structured graph, not opaque binary — ghost cursors have something semantic to anchor to.
- Audience is game devs, so gamified UX feels native rather than gimmicky.

## Staged roadmap

Each stage is independently shippable and useful. The CRDT cliff only appears at stage 5, and is optional.

### 1. Presence only

- Lightweight WebSocket server (single Go/Node binary, self-hostable).
- Plugin emits `user X opened file Y` / `closed file Y` via `EditorPlugin` signals.
- Panel in editor listing online teammates and their open files.
- Discord Rich Presence as a freebie ("Editing player.tscn in MyGame").

### 2. Conflict warnings

- "Jessey is editing `player.tscn` right now — open anyway?" modal.
- Status colours: green = viewing, yellow = selected, red = modified in last 30s.
- Optional `pre-commit` hook that warns when committing files a teammate recently touched.
- _Social_ locking, not enforced — no admin, no lock-recovery problems.

### 3. Ghost cursors (read-only)

- Broadcast `(user_id, selected_node_path, viewport_camera_transform)` at ~10Hz.
- Render translucent overlays in other clients' viewports.
- No mutation = no sync conflicts. First real engineering problem: gracefully handling "the node my ghost was anchored to just got deleted."

### 4. Gamification polish

- Avatars in the FileSystem dock next to whichever file each teammate has open.
- Activity feed styled like a Quake killfeed ("Jessey committed 3 changes to player.gd").
- "Session" concept — see what changed during a coworking block.

### 5. _(Optional, much later)_ Live property co-editing

- Only for safe surfaces (inspector leaf values: numbers, colors, strings).
- Never touch the scene tree structure itself.
- This is the CRDT step — don't commit unless stages 1–4 proved demand.

## Architecture decisions to make early

|Concern|Recommendation|
|---|---|
|Transport|WebSocket, not WebRTC. NAT/TURN is a tax not worth paying for a presence MVP.|
|Hosting|Self-hostable Docker container. Godot community is allergic to mandatory SaaS.|
|Pairing|Hash `project.godot` (or a stable subset) → room ID. Auto-join, zero config.|
|Auth|None for MVP; layer on later if team scoping is needed.|
|State model|Ephemeral pub/sub for stages 1–4. Persistence only for activity log.|

## Naming

`GodotTogether` is taken (existing experimental plugin, not production-ready). **Co-op Mode** fits the audience — activity feed = killfeed, ghost cursors = spectators, the framing writes itself.

## Prior art to study

- **VS Code Live Share** — clean awareness/document split, CRDT-based text co-editing. Useful reference for stage 5.
- **Figma multiplayer** — best-in-class awareness UX. Read their engineering blog posts on cursor presence.
- **Unreal Multi-User Editing** — authoritative-server model with operation replication. Closest existing thing in game-engine land.
- **Unity Collaborate (RIP)** — cautionary tale. Conflated session state with VCS state; that's the mistake to avoid.

## Open questions

- Should ghost cursors include voice/text chat, or stay out of comms entirely and let Discord do its job?
- Is there value in a "spectator mode" where someone joins read-only without opening the project locally? (Useful for code review / mentoring.)
- How does this interact with `git` branches? If Jessey is on `feature/inventory` and I'm on `main`, do we see each other's presence or not? (Probably yes for presence, no for ghost cursors — different scene state.)