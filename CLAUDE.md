# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Archery Legends** — A monetized Roblox archery game with cosmetic-first monetization and engagement-optimized retention mechanics.

| Attribute | Value |
|-----------|-------|
| Phase | MVP — Phase 6 (Game Modes) |
| Engine | Roblox Studio + Luau |
| MCP | robloxstudio-mcp (direct Studio manipulation) |
| Code Location | **Roblox Studio** (not local files) |

## Quick Start

```bash
# 1. Start session (loads context, checks Studio connection)
/start-session

# 2. Current priorities are in:
cat _ops/NEXT_STEPS.md
```

**Common MCP operations:**
```
get_place_info                          # Verify Studio connection
get_project_structure scriptsOnly=true  # See all scripts
get_script_source instancePath="game.ServerScriptService.GameManager"
start_playtest mode="play"              # Test changes
get_playtest_output                     # Check for errors
stop_playtest                           # End test
```

## Architecture

**All game logic lives in Roblox Studio.** Local files are documentation only.

### Server Scripts (ServerScriptService)
| Script | Responsibility |
|--------|----------------|
| GameManager | Round lifecycle, arrow physics, hit detection, scoring |
| DataManager | DataStore persistence, XP/currency awards, level-ups |
| DailyRewardManager | Streak tracking, reward distribution |
| LeaderboardManager | OrderedDataStore rankings (daily/weekly/all-time) |
| ShopManager | Purchase validation, inventory management |

### Client Scripts (StarterPlayerScripts)
| Script | Responsibility |
|--------|----------------|
| BowController | Aim, draw, release input; trajectory preview |
| HUDController | Score, arrows, XP bar, round summary |
| DailyRewardController | Claim UI, 7-day calendar |
| LeaderboardController | Tab interface, top 50 display |
| ShopController | Item grid, purchase/equip flow |

### Shared Modules (ReplicatedStorage/Modules)
| Module | Contents |
|--------|----------|
| Config | Constants: physics, scoring zones, XP curves, shop items, daily rewards |
| Types | PlayerData type definition, GetDefaultPlayerData() |

### Remotes (ReplicatedStorage/Remotes)
Fire-and-forget: `FireArrow`, `ArrowResult`, `RoundEnd`, `DailyRewardStatus`, `LeaderboardUpdated`
Request-response: `GetPlayerData`, `ClaimDailyReward`, `GetLeaderboard`, `GetShopData`, `PurchaseItem`, `EquipItem`

## Development Workflow

```
Inspect → Edit → Verify → Playtest → Fix → Update PROGRESS.md
```

1. **Inspect:** Read current state with `get_script_source` before any edit
2. **Edit:** Use `edit_script_lines` for targeted changes, `set_script_source` for new scripts
3. **Verify:** ALWAYS `get_script_source` after edit to confirm it applied
4. **Playtest:** `start_playtest` → poll `get_playtest_output` → `stop_playtest`
5. **Fix:** Loop until zero errors. Never proceed with broken code.
6. **Document:** Update `_ops/PROGRESS.md` after significant changes

## Luau Conventions

- `local` for all variables (no globals)
- Type annotations: `function foo(bar: number): string`
- `pcall()` wraps DataStore/HTTP calls
- File suffixes: `.server.luau`, `.client.luau`, `.luau` (modules)
- `task.spawn()` / `task.wait()` (not deprecated `spawn()` / `wait()`)
- RemoteEvents for fire-and-forget, RemoteFunctions only when return needed

## Security Model

| Rule | Implementation |
|------|----------------|
| Server-authoritative | All currency, XP, inventory logic on server |
| Client sends intent | Direction + power only, never scores |
| Input validation | Bounds check, type check, sanitize all remotes |
| Rate limiting | 0.5s cooldown per remote fire |
| DataStore throttle | Debounced saves (6s min), save on round-end |

## Work Order (Mandatory)

```
Core mechanics → Security → Persistence → Progression → Monetization → UI
```

**Phases 1-5 complete.** Current: Game Modes (Duel, Practice, Game Passes)

## Monetization Rules

- **Cosmetic-only.** Zero gameplay advantages for Robux.
- Game Passes: VIP (2x XP), Double Currency, Radio
- Developer Products: Bow skins, arrow trails, emotes
- Receipt processing via `MarketplaceService.ProcessReceipt` with idempotency

## Verification Checklist

Before marking any task complete:

- [ ] `get_script_source` confirms edit applied
- [ ] `start_playtest` — no syntax errors
- [ ] `get_playtest_output` — no runtime errors
- [ ] Feature works as intended
- [ ] `stop_playtest` — clean exit

## Local Files

```
_ops/PROGRESS.md      # Completed work log (update after changes)
_ops/NEXT_STEPS.md    # Current priorities
docs/game-design-document.md  # Full GDD with mechanics, modes, monetization
docs/engagement-psychology.md # Retention mechanics design
```

## Troubleshooting

| Issue | Fix |
|-------|-----|
| MCP not connecting | Check Roblox Studio running, MCP plugin active |
| DataStore errors in playtest | Enable "Studio Access to API Services" in Game Settings → Security |
| Script not updating | Use `get_script_source` to verify, check instancePath |
| Playtest hangs | `stop_playtest`, check for infinite loops |

## Skills Reference

For detailed MCP tool documentation, patterns, and examples, invoke the `roblox-studio-expert` skill.
