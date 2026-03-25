# Archery Legends — Project Status

**Last Updated:** 2026-03-25
**Current Phase:** MVP — Phase 2: Core Mechanic
**Playtest Status:** PASSING (zero errors)

---

## Quick Status

| Component | Status | Progress |
|-----------|--------|----------|
| Foundation | COMPLETE | Arena, target, Config, Types, Remotes |
| Visual Polish | COMPLETE | Terrain, particles, torches, lighting |
| Core Mechanic | IN PROGRESS | BowController ✓, Arrow flight ✓, Hit detection ✓, Round lifecycle pending |
| Data Persistence | NOT STARTED | — |
| Game Modes | NOT STARTED | — |
| UI/HUD | NOT STARTED | — |

---

## Roblox Studio Hierarchy

```
game
├── Workspace/
│   ├── Arenas/
│   │   ├── firing_platform (25 parts)
│   │   ├── arena_fencing (42 parts)
│   │   ├── spectator_area (46 parts)
│   │   ├── decorations (69 parts)
│   │   ├── trees_fixed (30 parts)
│   │   ├── archery_target_v2 (8 parts + effects)
│   │   ├── arena_ground (5 parts)
│   │   └── ground_details (15 parts)
│   ├── Torches/ (10 torches with fire/smoke/sparks/lights)
│   ├── AtmosphericEffects/ (dust, leaves, pollen)
│   ├── SpawnLocations/FiringPlatformSpawn
│   └── Terrain (grass, dirt, sand, slate, rock, water)
│
├── ReplicatedStorage/
│   ├── Modules/
│   │   ├── Config.luau (game constants)
│   │   └── Types.luau (type definitions)
│   ├── Remotes/ (10 RemoteEvents + 2 RemoteFunctions)
│   └── Assets/ (empty, for bow/arrow models)
│
├── ServerScriptService/
│   └── GameManager.server.luau (arrow flight, hit detection, scoring)
├── StarterPlayer/StarterPlayerScripts/
│   └── BowController.client.luau (aim, draw, fire input)
└── StarterGui/ (folders created: HUD, ShopGui, etc.)
```

---

## Next Immediate Tasks

1. **BowController.client.luau** — Mouse aim tracking, draw mechanic, power meter
2. **ArrowFlight** — Server-side physics and hit detection
3. **GameManager.server.luau** — Round lifecycle and scoring

---

## Manual Steps Required

See `_ops/MANUAL_STEPS.md` for tasks requiring manual Studio action.

**Current:** Add ambient audio via Studio Audio Library

---

## Links

| Resource | Path |
|----------|------|
| Full Progress Log | `_ops/PROGRESS.md` |
| Next Steps Detail | `_ops/NEXT_STEPS.md` |
| Game Design Doc | `docs/game-design-document.md` |
| MVP Task List | `docs/mvp-task-list.md` |
| Manual Steps | `_ops/MANUAL_STEPS.md` |
