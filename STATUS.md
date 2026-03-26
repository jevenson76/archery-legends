# Archery Legends — Project Status

**Last Updated:** 2026-03-26
**Current Phase:** MVP — Phase 5 COMPLETE, Ready for Phase 6: Game Modes
**Playtest Status:** PASSING (zero errors, 10 scripts)

---

## Quick Status

| Component | Status | Progress |
|-----------|--------|----------|
| Foundation | COMPLETE | Arena, target, Config, Types, Remotes |
| Visual Polish | COMPLETE | Terrain, particles, torches, lighting |
| Core Mechanic | COMPLETE | BowController ✓, Arrow flight ✓, Hit detection ✓, Round lifecycle ✓ |
| UI/HUD | COMPLETE | Score, arrows, hit feedback, round summary, XP bar |
| Data Persistence | COMPLETE | DataManager ✓, Auto-save ✓, XP/Currency awards ✓ |
| Progression | COMPLETE | XP bar ✓, Daily rewards ✓, Leaderboards ✓ |
| **Monetization/UI** | **COMPLETE** | Daily Reward UI ✓, Leaderboard UI ✓, Shop system ✓ |
| Game Modes | NOT STARTED | Quick Match, Duel, Practice |

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
│   ├── Remotes/ (10 RemoteEvents + 7 RemoteFunctions)
│   └── Assets/ (empty, for bow/arrow models)
│
├── ServerScriptService/
│   ├── GameManager.server.luau (rounds, arrow flight, hit detection, scoring)
│   ├── DataManager.server.luau (DataStore, XP, currency, persistence)
│   ├── DailyRewardManager.server.luau (daily login rewards, streaks)
│   ├── LeaderboardManager.server.luau (OrderedDataStore rankings)
│   └── ShopManager.server.luau (purchase processing, item ownership)
├── StarterPlayer/StarterPlayerScripts/
│   ├── BowController.client.luau (aim, draw, fire input)
│   ├── HUDController.client.luau (score, arrows, feedback, XP/currency)
│   ├── DailyRewardController.client.luau (7-day calendar, claim popup)
│   ├── LeaderboardController.client.luau (top 50, tabs, auto-refresh)
│   └── ShopController.client.luau (bow skins, arrow trails, purchase)
└── StarterGui/ (folders created: HUD, ShopGui, etc.)
```

---

## Next Immediate Tasks

1. **1v1 Duel Mode** — Real-time competitive archery matches
2. **Game Passes** — VIP, Double XP, Radio pass via MarketplaceService
3. **Practice Mode** — Unlimited arrows, no scoring pressure

---

## Manual Steps Required

See `_ops/MANUAL_STEPS.md` for tasks requiring manual Studio action.

**Current:**
- Enable Studio DataStore Access (Game Settings → Security)
- Add ambient audio via Studio Audio Library

---

## Links

| Resource | Path |
|----------|------|
| Full Progress Log | `_ops/PROGRESS.md` |
| Next Steps Detail | `_ops/NEXT_STEPS.md` |
| Game Design Doc | `docs/game-design-document.md` |
| MVP Task List | `docs/mvp-task-list.md` |
| Manual Steps | `_ops/MANUAL_STEPS.md` |
