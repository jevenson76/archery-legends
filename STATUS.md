# Archery Legends — Project Status

**Last Updated:** 2026-03-25
**Current Phase:** MVP — Phase 2 COMPLETE, Ready for Phase 3: Data Persistence
**Playtest Status:** PASSING (zero errors)

---

## Quick Status

| Component | Status | Progress |
|-----------|--------|----------|
| Foundation | COMPLETE | Arena, target, Config, Types, Remotes |
| Visual Polish | COMPLETE | Terrain, particles, torches, lighting |
| Core Mechanic | COMPLETE | BowController ✓, Arrow flight ✓, Hit detection ✓, Round lifecycle ✓ |
| UI/HUD | COMPLETE | Score display, arrows remaining, hit feedback, round summary |
| Data Persistence | NOT STARTED | — |
| Game Modes | NOT STARTED | — |

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
│   ├── BowController.client.luau (aim, draw, fire input)
│   └── HUDController.client.luau (score, arrows, feedback, round summary)
└── StarterGui/ (folders created: HUD, ShopGui, etc.)
```

---

## Next Immediate Tasks

1. **DataManager.server.luau** — DataStore setup for player data persistence
2. **Auto-save system** — Save on round end, load on join
3. **XP and leveling** — Earn XP from scoring, level up rewards

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
