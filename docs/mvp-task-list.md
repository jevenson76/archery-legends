# Archery Legends — MVP Build Plan

**Total Estimated Time:** 36-48 hours (18-24 sessions at 2-3 hours each)
**Target Completion:** 3-4 weeks

---

## Phase 1: Foundation (Days 1-2)

### Day 1: Arena & Project Structure
**Time:** 2-3 hours

**What to Build:**
- Flat arena ground plane (100x100 studs)
- Firing line position marker
- Target stand at 30 studs distance
- Target model with 4 concentric zones (Bullseye/Inner/Outer/Edge)
- SpawnLocation at firing line
- Complete folder structure matching CLAUDE.md

**MCP Tools:**
- `get_project_structure` — see current Studio state
- `create_object` — arena parts, target zones
- `mass_create_objects` — folder hierarchy
- `set_property` — colors, sizes, positions
- `get_file_tree` — verify structure

**Definition of Done:**
- [ ] Player spawns at firing line facing target
- [ ] Target visible with 4 distinct colored zones
- [ ] All folder structure exists (ServerScriptService, ReplicatedStorage/Modules, ReplicatedStorage/Remotes, etc.)
- [ ] Playtest shows correct spawn position

**Commands:**
```
get_project_structure → create arena → set_property for all parts →
get_file_tree → start_playtest → get_playtest_output → verify spawn
```

---

### Day 2: Config Module & Remotes
**Time:** 2 hours

**What to Build:**
- `ReplicatedStorage/Modules/Config.luau` with all tuning constants
- `ReplicatedStorage/Remotes/` folder with all RemoteEvents/Functions
- `ReplicatedStorage/Modules/Types.luau` with type definitions

**MCP Tools:**
- `create_object` — ModuleScripts, RemoteEvents, RemoteFunctions
- `set_script_source` — write module code
- `get_script_source` — verify content

**Definition of Done:**
- [ ] Config module exports all constants (arrow speed, gravity, points per zone, etc.)
- [ ] All Remotes from GDD exist (FireArrow, ArrowResult, RoundEnd, etc.)
- [ ] Types module defines PlayerData type
- [ ] No errors on playtest

**Config.luau Contents:**
```lua
-- Physics
ArrowSpeed = 100,
Gravity = 196.2,
MaxDrawTime = 1.5,
FireRateCooldown = 0.5,

-- Scoring
PointsPerZone = {Bullseye = 10, Inner = 7, Outer = 4, Edge = 1},
ZoneRadii = {Bullseye = 0.5, Inner = 1.5, Outer = 3.0, Edge = 4.5},

-- Difficulty
Difficulties = {
    Casual = {gravity = false, wind = false, distance = 20, xpMult = 1.0},
    Normal = {gravity = true, wind = false, distance = 30, xpMult = 1.5},
    Expert = {gravity = true, wind = true, distance = 40, xpMult = 2.0}
},

-- Progression
BaseXP = 50,
XPPerBullseye = 10,
CurrencyPerScorePoint = 0.2,
LevelCurveExponent = 1.5,
MaxLevel = 100,

-- Rounds
ArrowsPerRound = 10,
DuelArrowsPerPlayer = 5
```

---

## Phase 2: Core Mechanic (Days 3-6)

### Day 3: Bow Controller — Input & Aim
**Time:** 2-3 hours

**What to Build:**
- `StarterPlayerScripts/BowController.client.luau`
- Mouse aim tracking (bow follows cursor)
- Draw mechanic (hold LMB to charge power)
- Power meter visualization (0-100%)
- Aim arc trajectory preview

**MCP Tools:**
- `create_object` — LocalScript
- `set_script_source` — client code
- `start_playtest` / `get_playtest_output` — test input

**Definition of Done:**
- [ ] Holding left mouse button charges power (0→100% over 1.5s)
- [ ] Releasing fires (just logs for now, no server communication)
- [ ] Power meter visible on screen
- [ ] Aim arc shows predicted trajectory (using Config gravity value)
- [ ] No input lag or stuttering

---

### Day 4: Arrow Flight & Server Communication
**Time:** 2-3 hours

**What to Build:**
- Client: Send FireArrow event on release
- Server: `ServerScriptService/GameManager.server.luau` — receive and validate
- Server: Fire rate limiting (max 1 per 0.5s per player)
- Visual: Arrow spawns and flies along trajectory

**MCP Tools:**
- `edit_script_lines` — add to BowController
- `create_object` — GameManager server script
- `set_script_source` — server validation logic
- `start_playtest` — test round-trip

**Definition of Done:**
- [ ] Client sends FireArrow with direction, power, difficulty
- [ ] Server validates fire rate (spam protection)
- [ ] Server logs received shot data
- [ ] Arrow visual flies from player to target area
- [ ] No duplicate fires, no exploits

---

### Day 5: Hit Detection & Scoring
**Time:** 2-3 hours

**What to Build:**
- Server-side raycast from fire origin to target
- Zone detection (which ring was hit)
- Score calculation
- ArrowResult event back to client
- Client: score popup, hit particles, sound

**MCP Tools:**
- `edit_script_lines` — GameManager hit detection
- `get_script_source` — verify logic
- `create_object` — particle emitters, sounds
- `start_playtest` — test hit feedback

**Definition of Done:**
- [ ] Server correctly identifies hit zone (or miss)
- [ ] Score popup appears at impact point
- [ ] Particle burst on hit (gold for bullseye, etc.)
- [ ] Sound plays (higher pitch for better zones)
- [ ] Near-miss indicator shows distance when missed

---

### Day 6: Quick Match Round Logic
**Time:** 2-3 hours

**What to Build:**
- Round state machine (waiting → active → complete)
- Arrow counter (10 arrows per round)
- Cumulative score tracking
- RoundEnd event with totals
- XP and currency calculation

**MCP Tools:**
- `edit_script_lines` — GameManager round logic
- `get_script_source` — verify state machine
- `start_playtest` — play full round

**Definition of Done:**
- [ ] Round starts when player fires first arrow
- [ ] Arrow count decrements correctly (10→0)
- [ ] Score accumulates across all shots
- [ ] RoundEnd fires after 10th arrow with correct totals
- [ ] XP/currency calculated per Config formulas

---

## Phase 3: Data Persistence (Days 7-8)

### Day 7: DataStore Setup
**Time:** 2-3 hours

**What to Build:**
- `ServerScriptService/DataManager.server.luau`
- PlayerData schema (per Types.luau)
- Load on PlayerAdded with pcall + 3 retries
- Module functions: GetData, UpdateData, IncrementValue

**MCP Tools:**
- `create_object` — DataManager script
- `set_script_source` — DataStore logic
- `start_playtest` — test load/save

**Definition of Done:**
- [ ] Player data loads on join (or creates default if new)
- [ ] GetData returns player's current data table
- [ ] UpdateData successfully writes to DataStore
- [ ] 3 retry attempts on DataStore failure
- [ ] Error handling doesn't crash server

---

### Day 8: Auto-Save & Session Persistence
**Time:** 2-3 hours

**What to Build:**
- Auto-save every 120 seconds per player
- Save on PlayerRemoving
- BindToClose for server shutdown
- Wire GameManager to update stats after rounds
- Test: play round, leave, rejoin, verify data

**MCP Tools:**
- `edit_script_lines` — DataManager auto-save
- `edit_script_lines` — GameManager save integration
- `start_playtest` — join/leave/rejoin test

**Definition of Done:**
- [ ] Data persists across sessions
- [ ] Level, XP, currency update after rounds
- [ ] TotalGamesPlayed, TotalBullseyes, HighScore tracked
- [ ] No data loss on normal leave or server shutdown
- [ ] Playtest output shows DataStore operations succeeding

---

## Phase 4: 1v1 Duels (Days 9-11)

### Day 9: Duel Matchmaking
**Time:** 2-3 hours

**What to Build:**
- `ServerScriptService/DuelManager.server.luau`
- Simple queue system (first two players matched)
- RequestDuel event handling
- DuelState event broadcasting
- Match creation with both players

**MCP Tools:**
- `create_object` — DuelManager
- `set_script_source` — queue logic
- `start_playtest` — test with 2 players (use Studio multi-client)

**Definition of Done:**
- [ ] Player can request to join duel queue
- [ ] Two queued players get matched
- [ ] Both players receive DuelState with opponent info
- [ ] Queue handles edge cases (player leaves queue)

---

### Day 10: Duel Turn System
**Time:** 2-3 hours

**What to Build:**
- Alternating turn logic (Player A → Player B → A → B...)
- Turn indicator UI
- Score tracking for both players
- Arrow count per player (5 each)
- Winner determination

**MCP Tools:**
- `edit_script_lines` — DuelManager turn logic
- `create_object` — turn indicator UI
- `start_playtest` — play full duel

**Definition of Done:**
- [ ] Turns alternate correctly
- [ ] Non-active player cannot fire
- [ ] Scores tracked separately
- [ ] Match ends after 10 total arrows (5 each)
- [ ] Winner announced (ties: most bullseyes wins)

---

### Day 11: Duel Rewards & Ranking
**Time:** 2 hours

**What to Build:**
- Win/loss XP and currency multipliers
- Rank point adjustment
- Post-duel results screen
- Update player stats (DuelsWon, DuelsLost)

**MCP Tools:**
- `edit_script_lines` — DuelManager rewards
- `edit_script_lines` — DataManager rank update
- `start_playtest` — verify rewards

**Definition of Done:**
- [ ] Winner gets 2x rewards, loser gets 0.5x
- [ ] Rank points adjust (+25 win, -15 loss)
- [ ] Stats update in DataStore
- [ ] Results screen shows XP/currency earned

---

## Phase 5: Engagement Systems (Days 12-14)

### Day 12: Daily Rewards
**Time:** 2-3 hours

**What to Build:**
- `ServerScriptService/DailyRewardManager.server.luau`
- Streak logic (increment on new day, reset on miss)
- 7-day reward cycle with escalating value
- DailyRewardClaim/Result events
- Popup UI on join

**MCP Tools:**
- `create_object` — DailyRewardManager, UI
- `set_script_source` — streak logic
- `start_playtest` — claim reward

**Definition of Done:**
- [ ] New day increments streak
- [ ] Missed day resets streak to 1
- [ ] Correct reward granted per day (currency/items)
- [ ] Popup shows on join with claim button
- [ ] Claimed status persists (can't claim twice same day)

---

### Day 13: Leaderboards
**Time:** 2-3 hours

**What to Build:**
- `ServerScriptService/LeaderboardManager.server.luau`
- OrderedDataStore for Daily, Weekly, All-Time
- Update leaderboard after each round
- GetLeaderboard RemoteFunction
- Leaderboard UI panel

**MCP Tools:**
- `create_object` — LeaderboardManager
- `set_script_source` — OrderedDataStore logic
- `create_object` — leaderboard UI
- `start_playtest` — verify entries

**Definition of Done:**
- [ ] High scores save to correct leaderboard
- [ ] Daily/weekly keys include date for rotation
- [ ] Client can request top 50 entries
- [ ] UI displays rank, name, score
- [ ] Own rank highlighted if in top 50

---

### Day 14: Practice Range
**Time:** 2 hours

**What to Build:**
- Practice mode flag in GameManager
- No scoring, no XP, no DataStore writes
- Unlimited arrows
- Difficulty selector UI
- Distance slider (10-50 studs)

**MCP Tools:**
- `edit_script_lines` — GameManager practice mode
- `create_object` — practice UI elements
- `start_playtest` — practice without saving

**Definition of Done:**
- [ ] Practice mode doesn't affect stats
- [ ] Can switch difficulty on the fly
- [ ] Distance slider moves target
- [ ] Trajectory guide always visible
- [ ] Exit practice returns to lobby

---

## Phase 6: UI Polish (Days 15-17)

### Day 15: HUD
**Time:** 2-3 hours

**What to Build:**
- `StarterGui/HUD/` complete implementation
- Score display (current round)
- XP bar with level indicator
- Arrow counter
- Difficulty indicator
- Streak counter (if applicable)

**MCP Tools:**
- `create_object` — UI frames, labels
- `set_property` — positioning, styling
- `edit_script_lines` — UIController updates
- `start_playtest` — visual verification

**Definition of Done:**
- [ ] All HUD elements visible and positioned correctly
- [ ] Score updates in real-time on hits
- [ ] XP bar animates on gain
- [ ] Arrow counter decrements
- [ ] Clean, readable design

---

### Day 16: Results & Popups
**Time:** 2-3 hours

**What to Build:**
- End-of-round results screen
- XP gained, currency gained, new level animation
- "Play Again" button
- Daily reward popup (if not already polished)
- Duel results screen

**MCP Tools:**
- `create_object` — result UI frames
- `edit_script_lines` — UIController result handling
- `start_playtest` — full flow test

**Definition of Done:**
- [ ] Results screen shows after every round
- [ ] Level up animation plays when applicable
- [ ] "Play Again" returns to ready state
- [ ] Duel results show winner clearly
- [ ] All popups dismissible

---

### Day 17: Menu & Mode Selection
**Time:** 2-3 hours

**What to Build:**
- Main menu / lobby UI
- Mode selection (Quick Match, 1v1, Practice)
- Difficulty selection
- Settings (volume placeholder)
- Leaderboard access button

**MCP Tools:**
- `create_object` — menu UI
- `edit_script_lines` — menu logic
- `start_playtest` — navigate all menus

**Definition of Done:**
- [ ] Clean main menu on spawn
- [ ] All three modes accessible
- [ ] Difficulty selection works
- [ ] Leaderboard opens correctly
- [ ] Smooth transitions between states

---

## Phase 7: Testing & Launch Prep (Days 18-20)

### Day 18: Bug Fixing & Edge Cases
**Time:** 2-3 hours

**What to Build:**
- Fix all errors found in playtest output
- Handle edge cases (disconnect during duel, rapid firing, etc.)
- Validate all DataStore operations
- Test on multiple accounts

**MCP Tools:**
- `get_playtest_output` — find errors
- `grep_scripts` — search for issues
- `edit_script_lines` — fix bugs
- `start_playtest` — verify fixes

**Definition of Done:**
- [ ] Zero errors in playtest output
- [ ] Zero warnings related to game logic
- [ ] All edge cases handled gracefully
- [ ] Data integrity maintained

---

### Day 19: Performance & Polish
**Time:** 2-3 hours

**What to Build:**
- Optimize particle effects
- Reduce unnecessary remote traffic
- Improve UI responsiveness
- Add loading states where needed

**MCP Tools:**
- `get_playtest_output` — check for lag
- `edit_script_lines` — optimizations
- `start_playtest` — performance test

**Definition of Done:**
- [ ] Smooth 60fps gameplay
- [ ] No network congestion
- [ ] UI feels snappy
- [ ] Memory usage stable over long sessions

---

### Day 20: Final Playtest & Documentation
**Time:** 2 hours

**What to Build:**
- Full playthrough from new player perspective
- Document any remaining issues
- Update CLAUDE.md if structure changed
- Prepare for friends & family test

**MCP Tools:**
- `start_playtest` — full session
- `get_project_structure` — verify final state

**Definition of Done:**
- [ ] Complete new player flow works
- [ ] All MVP features functional
- [ ] Documentation current
- [ ] Ready for external testing

---

## MVP Completion Checklist

### Core Mechanic
- [ ] Aim and draw bow
- [ ] Arrow physics (Casual + Normal)
- [ ] Hit detection with 4 zones
- [ ] Visual/audio feedback

### Game Modes
- [ ] Quick Match (10 arrows)
- [ ] 1v1 Duel (alternating, 5 each)
- [ ] Practice Range (unlimited)

### Progression
- [ ] XP and leveling
- [ ] Currency earning
- [ ] Data persistence

### Engagement
- [ ] Daily rewards with streak
- [ ] Leaderboards (daily/weekly/all-time)

### UI
- [ ] HUD
- [ ] Results screen
- [ ] Daily reward popup
- [ ] Mode selection menu
- [ ] Leaderboard view

---

## Risk Mitigation

| Risk | Mitigation |
|------|------------|
| Arrow physics feels bad | Day 5 buffer for tuning. Can simplify to Casual-only if needed. |
| Duel matchmaking issues | Simple queue first. Skip skill-based matching for MVP. |
| DataStore rate limits | Debounce saves, batch updates. 120s auto-save is conservative. |
| 1v1 sync problems | Server authoritative. Client shows predicted state, corrects on server response. |
| Scope creep | Explicit "deferred" list. No shop, no battle pass, no badges in MVP. |

---

## Post-MVP Roadmap (Weeks 5-8)

1. **Week 5:** Expert difficulty (wind), shop with 3 bows and 3 trails
2. **Week 6:** Weekly challenges, badges
3. **Week 7:** Battle pass (free track only initially)
4. **Week 8:** Second arena, tournament mode prototype
