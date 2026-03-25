# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Archery Legends** — A monetized, high-engagement archery game on Roblox. Solo developer build targeting top-chart retention metrics with cosmetic-first monetization.

**Current Phase:** MVP (core mechanic, basic scoring, one arena, data persistence)

## Tech Stack

- **Engine:** Roblox Studio + Luau (Roblox's Lua 5.1 derivative)
- **MCP Integration:** robloxstudio-mcp (39+ tools for direct Studio manipulation)
- **Persistence:** DataStore, OrderedDataStore for leaderboards
- **Monetization:** MarketplaceService (cosmetic-only)

## Development Workflow

**All game code lives in Roblox Studio, not local files.** Use MCP tools for all interactions.

```
1. Inspect current state (get_script_source, get_project_structure)
       ↓
2. Write/edit code via MCP (set_script_source, edit_script_lines)
       ↓
3. Verify edit applied (get_script_source to confirm)
       ↓
4. Playtest (start_playtest → get_playtest_output → stop_playtest)
       ↓
5. Fix errors and re-test until clean
       ↓
6. Update _ops/PROGRESS.md
```

## MCP Tools Reference

**Inspect (read-only):**
- `get_project_structure` — Full hierarchy tree
- `get_script_source` — Read script code (use before/after edits)
- `grep_scripts` — Search all scripts for patterns
- `get_instance_properties` — Get instance configuration
- `search_objects` — Find instances by name/class

**Modify (write):**
- `set_script_source` — Replace entire script (for new scripts)
- `edit_script_lines` — Replace specific line range (for targeted fixes)
- `insert_script_lines` — Add lines at position
- `delete_script_lines` — Remove line range
- `create_object` — Create new instance
- `delete_object` — Remove instance
- `set_property` / `mass_set_property` — Configure properties

**Build Library:**
- `generate_build` — Procedural build via JS code
- `create_build` — Define build from part arrays
- `import_build` — Place build in Studio
- `list_library` — Browse saved builds

**Test:**
- `start_playtest` — Begin play mode ("play") or server-only ("run")
- `get_playtest_output` — Poll logs for errors
- `stop_playtest` — End playtest, get final output

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

## Work Order

Always work in this order (per PROJECT_OPERATING_MODEL.md):

```
1. Core mechanics (shooting, scoring)
       ↓
2. Server security (validation, anti-cheat)
       ↓
3. Data persistence (DataStore)
       ↓
4. Progression systems (XP, levels)
       ↓
5. Monetization hooks
       ↓
6. UI polish (LAST)
```

**If a task attempts UI before core mechanics are stable, redirect to core work first.**

## Verification Checklist

Before marking any script task complete:

1. `get_script_source` — Confirm edit applied correctly
2. `start_playtest` — No syntax errors
3. `get_playtest_output` — No runtime errors
4. Feature works as intended
5. `stop_playtest` — Clean exit

**Never proceed to next task with broken/erroring code.**

## Local File Structure

```
/home/jevenson/dev/_pet_projects/roblox/
├── CLAUDE.md                -- This file
├── _ops/                    -- Operational tracking
│   ├── BOOT.md              -- Document authority hierarchy
│   ├── PROJECT_OPERATING_MODEL.md -- What this project is
│   ├── PROJECT_IDENTITY.md  -- Project context & scope
│   ├── PROGRESS.md          -- Completed work log
│   └── NEXT_STEPS.md        -- Current priorities
├── docs/
│   ├── game-design-document.md  -- Full GDD
│   ├── engagement-psychology.md -- Retention mechanics
│   └── mvp-task-list.md         -- 20-day phased build plan
└── .claude/
    ├── commands/            -- Slash commands (/start-session)
    └── skills/              -- Development skills
```

## Session Protocol

1. Run `/start-session` to initialize context
2. Check `_ops/NEXT_STEPS.md` for current priority
3. Verify Studio connection via `get_place_info`
4. Work in MCP loop (inspect → edit → verify → playtest → fix)
5. Update `_ops/PROGRESS.md` after significant changes

## Reference Documents

| Document | Purpose |
|----------|---------|
| `_ops/PROGRESS.md` | WHERE we are |
| `_ops/NEXT_STEPS.md` | WHERE we go next |
| `docs/game-design-document.md` | WHAT to build |
| `docs/engagement-psychology.md` | WHY we build it |
