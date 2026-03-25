# PROJECT IDENTITY: Archery Legends — Roblox Game

**Document Created:** 2026-03-25
**Analysis Type:** Project Blueprint
**Project Root:** `/home/jevenson/dev/_pet_projects/roblox`
**Game Title:** Archery Legends

---

## 1. What This Project Is

### Game Concept

A **monetized, high-engagement archery game** on Roblox. Solo developer build targeting top-chart retention metrics with cosmetic-first monetization and an addictive core loop.

**Elevator Pitch:** "Flappy Bird meets eSports" — simple to pick up, impossible to master.

### Target Metrics

| Metric | Target | Why |
|--------|--------|-----|
| D1 Retention | 40%+ | First-day hook matters most |
| D7 Retention | 20%+ | Weekly challenge loop working |
| Avg Session Time | 12+ minutes | 3-4 rounds per session |
| % Monetized Players | 5%+ | Cosmetic appeal landing |

### Revenue Model

**Cosmetic-only monetization. Zero gameplay advantages for Robux.**

| Revenue Stream | Examples |
|---------------|----------|
| Game Passes (one-time) | VIP (299R), Double Currency (149R), Radio (99R) |
| Developer Products (repeatable) | Arrow trails (49-199R), Bow skins (149-799R) |
| Battle Pass | 399R/season, 30-day seasons |

---

## 2. Technical Architecture

### Development Stack

| Layer | Technology |
|-------|------------|
| Game Engine | Roblox Studio |
| Language | Luau (Roblox's Lua 5.1 derivative) |
| MCP Integration | robloxstudio-mcp (39+ tools) |
| Persistence | Roblox DataStore, OrderedDataStore |
| Monetization | MarketplaceService |

### MCP-Driven Workflow

This project uses **robloxstudio-mcp** for direct Studio integration:

```
Local Planning → MCP Tools → Roblox Studio → Playtest → Fix → Repeat
```

**Key MCP Tools:**
- **Build & Edit:** `create_object`, `set_property`, `set_script_source`, `edit_script_lines`
- **Inspect:** `get_file_tree`, `get_script_source`, `get_project_structure`, `grep_scripts`
- **Test:** `start_playtest`, `get_playtest_output`, `stop_playtest`
- **Library:** `export_build`, `import_build`, `list_library`

### Roblox Studio Hierarchy

```
game
├── ServerScriptService/
│   ├── GameManager.server.luau       -- Round lifecycle, scoring, hit detection
│   ├── DuelManager.server.luau       -- 1v1 matchmaking, turn sync
│   ├── DataManager.server.luau       -- DataStore CRUD, auto-save
│   ├── ShopManager.server.luau       -- ProcessReceipt, purchase validation
│   ├── LeaderboardManager.server.luau-- OrderedDataStore rankings
│   ├── ChallengeManager.server.luau  -- Weekly challenge tracking
│   └── DailyRewardManager.server.luau-- Streak logic, reward grants
│
├── ReplicatedStorage/
│   ├── Modules/
│   │   ├── Config.luau               -- All tuning constants
│   │   ├── ArrowPhysics.luau         -- Trajectory calculation (shared)
│   │   └── Types.luau                -- Type definitions
│   ├── Remotes/                      -- RemoteEvents + RemoteFunctions
│   └── Assets/                       -- Bows, arrows, effects
│
├── StarterPlayerScripts/
│   ├── BowController.client.luau     -- Input handling, aim, fire
│   ├── CameraController.client.luau  -- Aim camera, spectate camera
│   └── UIController.client.luau      -- HUD updates, shop, popups
│
├── StarterGui/
│   ├── HUD/                          -- Score, XP bar, streak, challenges
│   ├── ShopGui/                      -- Bow/trail store
│   ├── ProgressionGui/               -- Level, battle pass
│   ├── DailyRewardGui/               -- Calendar popup
│   ├── DuelGui/                      -- Matchmaking, turn indicator
│   └── ResultsGui/                   -- End-of-round summary
│
└── Workspace/
    ├── Arenas/                       -- Playable maps
    ├── Targets/                      -- Target objects with zones
    └── SpawnLocations/
```

---

## 3. Game Design Summary

### Core Mechanic

1. **Aim:** Mouse position controls bow angle
2. **Draw:** Hold LMB to build power (0-100% over 1.5s)
3. **Release:** Let go to fire

### Difficulty Tiers

| Difficulty | Gravity | Wind | Distance | XP Multiplier |
|------------|---------|------|----------|---------------|
| Casual | None | None | 20 studs | 1.0x |
| Normal | Yes | None | 30 studs | 1.5x |
| Expert | Yes | Yes | 40 studs | 2.0x |

### Scoring Zones

| Zone | Radius | Points |
|------|--------|--------|
| Bullseye | 0.5 studs | 10 |
| Inner Ring | 1.5 studs | 7 |
| Outer Ring | 3.0 studs | 4 |
| Edge | 4.5 studs | 1 |
| Miss | >4.5 studs | 0 |

### Game Modes (MVP)

| Mode | Players | Arrows | Description |
|------|---------|--------|-------------|
| Quick Match | 1 | 10 | Solo, maximize score |
| 1v1 Duel | 2 | 5 each | Alternating turns, highest score wins |
| Practice Range | 1 | Unlimited | No scoring, skill building |

### Progression Systems

- **XP & Leveling:** Level 1-100, prestige to 10
- **Skill Ranking:** Bronze → Silver → Gold → Diamond → Legend
- **Daily Rewards:** 7-day cycle with escalating value
- **Weekly Challenges:** 3 active, refresh Monday
- **Battle Pass:** 40 tiers, 30-day seasons

---

## 4. MVP Scope

### MVP Features (Target: 3-4 weeks)

**Core Mechanic:**
- Aim, draw, release bow
- Arrow physics (Casual + Normal difficulty)
- Hit detection with 4 scoring zones
- Visual/audio feedback

**Game Modes:**
- Quick Match (10 arrows, solo)
- 1v1 Duel (alternating turns, 5 arrows each)
- Practice Range (unlimited, no scoring)

**Progression:**
- XP and leveling (to 100)
- Currency earning
- DataStore persistence

**Engagement:**
- Daily rewards with streak
- Leaderboards (daily/weekly/all-time)

**UI:**
- HUD (score, XP bar, difficulty indicator)
- Results screen
- Daily reward popup
- Leaderboard view

### Explicitly Deferred (Post-MVP)

- Expert difficulty (wind physics)
- Battle Pass system
- Shop and monetization
- Weekly challenges
- Badges
- Second arena
- All cosmetics beyond default
- Clans, Tournaments

---

## 5. Security Model

**All currency, XP, inventory, and progression logic runs on SERVER only.**

| Principle | Implementation |
|-----------|----------------|
| Server authority | Server calculates hit detection and scoring |
| Client sends intent | "I released arrow at angle X, power Y" |
| Server validates | Server processes and returns result |
| Rate limiting | Ignore client fires faster than 1 per 0.5s |
| DataStore safety | Writes throttled with debounce |

---

## 6. Local File Structure

```
/home/jevenson/dev/_pet_projects/roblox/
├── CLAUDE.md                  -- Tech stack, conventions, verification
├── _ops/                      -- Operational tracking
│   ├── BOOT.md               -- Document hierarchy
│   ├── PROJECT_OPERATING_MODEL.md
│   ├── PROJECT_IDENTITY.md   -- This file
│   ├── PROGRESS.md           -- Completed work
│   ├── NEXT_STEPS.md         -- Priorities
│   ├── runbooks/             -- Execution procedures
│   └── staging/              -- Temporary data
├── docs/
│   ├── game-design-document.md   -- Full GDD
│   ├── engagement-psychology.md  -- Retention mechanics
│   └── mvp-task-list.md          -- Phase breakdown
├── builds/                    -- MCP build library exports
└── mcp-servers/               -- MCP server configuration
```

---

## 7. Key Personnel

| Role | Name |
|------|------|
| Solo Developer | Jason |
| AI Assistant | Claude Code |

---

## 8. Definition of Done (MVP)

1. Player can join, see tutorial, hit target, earn score
2. Player can play Quick Match and 1v1 Duel
3. XP, level, currency, and stats persist across sessions
4. Daily rewards work with streak tracking
5. Leaderboards display top 50 for daily/weekly/all-time
6. Zero critical errors in playtest output

---

## Document History

| Date | Author | Change |
|------|--------|--------|
| 2026-03-25 | Claude Code | Initial creation |
