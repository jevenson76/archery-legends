# Roblox Archery Game

## What This Is
A monetized, high-engagement archery game on Roblox. Solo developer build. Target: top-chart retention metrics, cosmetic-first monetization, addictive core loop.

## Tech Stack
- Roblox Studio + Luau (Roblox's Lua 5.1 derivative)
- robloxstudio-mcp (39 tools — direct Studio integration via MCP)
- DataStore for persistence, OrderedDataStore for leaderboards
- MarketplaceService for monetization

## MCP Integration
This project uses the robloxstudio-mcp server to interact with Roblox Studio directly. Key tools:

**Build & Edit:** `create_instance`, `delete_instance`, `set_property`, `mass_set_property`, `mass_create_objects_with_properties`, `edit_script`, `execute_luau`
**Inspect:** `get_file_tree`, `get_script_source`, `get_instance_properties`, `get_instance_children`, `search_objects`, `grep_scripts`, `get_project_structure`
**Test:** `start_playtest`, `get_playtest_output`, `stop_playtest`
**Library:** `export_build`, `import_build`, `create_build`, `list_library`

Workflow: write/edit scripts → inject into Studio via MCP → start_playtest → read output → fix → repeat. This loop can run autonomously.

## Project Structure (Roblox Studio Hierarchy)
```
game
├── ServerScriptService/
│   ├── GameManager.server.luau        -- Round lifecycle, scoring
│   ├── DataManager.server.luau        -- DataStore save/load
│   ├── ShopManager.server.luau        -- Purchase processing
│   └── LeaderboardManager.server.luau -- OrderedDataStore rankings
├── ReplicatedStorage/
│   ├── Modules/
│   │   ├── Config.luau                -- Shared constants (XP curves, pricing)
│   │   ├── ArrowPhysics.luau          -- Shared physics calculations
│   │   └── Types.luau                 -- Type definitions
│   ├── Remotes/                       -- RemoteEvents + RemoteFunctions
│   └── Assets/                        -- Bow/arrow models, UI templates
├── StarterPlayerScripts/
│   ├── BowController.client.luau      -- Aim, draw, release input
│   ├── CameraController.client.luau   -- Aim camera behavior
│   └── UIController.client.luau       -- HUD, shop, progression UI
├── StarterGui/
│   ├── HUD/                           -- Score, XP bar, streak counter
│   ├── ShopGui/                       -- Bow/arrow skin store
│   ├── ProgressionGui/                -- Level, mastery, battle pass
│   └── ResultsGui/                    -- End-of-round summary
└── Workspace/
    ├── Arenas/                        -- Playable maps
    ├── Targets/                       -- Target objects with zones
    └── SpawnLocations/
```

## Luau Conventions
- Use `local` for all variables. No globals.
- Type annotations on function signatures: `function foo(bar: number): string`
- `pcall()` wraps every DataStore and HTTP call. Always handle failure.
- Server scripts end in `.server.luau`, client in `.client.luau`, modules in `.luau`
- RemoteEvents for fire-and-forget, RemoteFunctions only when server→client return is needed
- Never trust client input. Validate and sanitize everything server-side.
- Use `task.spawn()` and `task.wait()` instead of deprecated `spawn()` and `wait()`

## Security Model
- All currency, XP, inventory, and progression logic runs on SERVER only
- Client sends intent ("I released the arrow at angle X, power Y"), server validates and processes
- Server calculates hit detection and scoring, sends result back to client
- RemoteEvent rate limiting: ignore client fires faster than 1 per 0.5 seconds
- DataStore writes throttled with debounce (save on round-end, not every action)

## Monetization Rules
- Cosmetic-only purchases. Zero gameplay advantages for Robux.
- Game Passes (one-time): VIP (2x XP + chat tag), Radio, Double Currency
- Developer Products (repeatable): Arrow trails, bow skins, emotes, target skins
- No direct loot box purchases. Randomized rewards are earn-only through gameplay.
- Receipt processing via MarketplaceService.ProcessReceipt with proper idempotency

## Engagement Systems to Implement
- Daily login rewards with escalating streak bonuses (reset on miss)
- Weekly challenge rotation (3 active, refreshes Monday)
- Season/battle pass: free + premium track, 30-day seasons
- Roblox badges at milestones (first game, 100 bullseyes, level 10, etc.)
- Leaderboards: daily, weekly, all-time, friends-only
- Post-match screen: always show XP gained, progress to next unlock, "Play Again" prominent
- First session: player hits a bullseye within 30 seconds (tutorial), gets free cosmetic within 60s

## Verification
After creating or editing scripts:
1. Use `get_script_source` to confirm the edit took
2. Use `start_playtest` → `get_playtest_output` → `stop_playtest` to test
3. Check output for errors/warnings before moving on
4. If errors, fix and re-test. Don't move to next task with broken code.

## Scope Control
This is a solo dev project. When a task grows beyond what can be built in one session:
- Flag it and suggest phasing
- Always deliver working code, not partial implementations
- MVP before polish. Ship the core loop first.

## Current Phase
MVP — Core archery mechanic, basic scoring, one arena, data persistence. No shop, no battle pass, no clans yet.

## Docs
Design documents live in `docs/` in this project folder. Reference `docs/game-design-document.md` for full game vision and `docs/engagement-psychology.md` for retention mechanics.
