# Archery Legends Next Steps

**Last Updated:** 2026-03-26
**Current Phase:** MVP — Phase 5: Monetization / UI Polish

---

## Immediate Priority

### 1. Daily Reward UI (Client)

Create popup for claiming daily rewards:

**Deliverables:**
- [ ] Modal popup in StarterGui/DailyRewardGui
- [ ] 7-day calendar grid showing reward progression
- [ ] Claim button with pulse animation
- [ ] Connect to ClaimDailyReward RemoteFunction
- [ ] Show on login if reward available

### 2. Leaderboard UI (Client)

Create leaderboard display:

**Deliverables:**
- [ ] Tab interface for Daily/Weekly/AllTime
- [ ] Scrolling list of top 50 players
- [ ] Highlight current player's rank
- [ ] Connect to GetLeaderboard RemoteFunction
- [ ] Auto-refresh every 60 seconds

### 3. Shop System (Server + Client)

Create cosmetic shop:

**Deliverables:**
- [ ] ShopManager.server.luau for purchase processing
- [ ] MarketplaceService integration
- [ ] Bow skins, arrow trails, emotes inventory
- [ ] Shop UI in StarterGui/ShopGui

---

## Completed Phases

### Phase 1: Foundation ✓

| Task | Status |
|------|--------|
| Arena ground plane (100x100 studs) | ✓ |
| Firing line marker + SpawnLocation | ✓ |
| Target with 4 scoring zones at 30 studs | ✓ |
| Config.luau with all constants | ✓ |
| Types.luau with PlayerData type | ✓ |
| All RemoteEvents/Functions | ✓ |
| Folder structure | ✓ |
| Playtest verification | ✓ |

### Phase 2: Core Mechanic ✓

| Task | Status |
|------|--------|
| Bow Controller — Input & Aim | ✓ |
| Arrow Flight & Server Communication | ✓ |
| Hit Detection & Scoring | ✓ |
| Round Lifecycle (10 arrows) | ✓ |
| HUD (score, arrows, feedback) | ✓ |
| Round End Summary | ✓ |

### Phase 3: Data Persistence ✓

| Task | Status |
|------|--------|
| DataManager with DataStore | ✓ |
| Load/save with retry logic | ✓ |
| Auto-save on round end | ✓ |
| XP/Currency awards | ✓ |
| BindToClose for shutdown | ✓ |

### Phase 4: Progression ✓

| Task | Status |
|------|--------|
| XP bar in HUD with animation | ✓ |
| DailyRewardManager (server) | ✓ |
| Streak tracking with reset | ✓ |
| LeaderboardManager (OrderedDataStore) | ✓ |
| Daily/Weekly/AllTime rankings | ✓ |

---

## Pending Implementation (per mvp-task-list.md)

### Phase 5: Monetization (Days 11-12)

| Task | Status | Reference |
|------|--------|-----------|
| Shop System | PENDING | Day 11 |
| Game Passes | PENDING | Day 12 |

### Phase 6: Polish & Game Modes (Days 13-16)

| Task | Status | Reference |
|------|--------|-----------|
| Daily Reward UI | PENDING | Day 13 |
| Leaderboard UI | PENDING | Day 14 |
| 1v1 Duel Mode | PENDING | Day 15-16 |

### Phase 7: See mvp-task-list.md

Full 20-day plan in `docs/mvp-task-list.md`

---

## Work Order Reminder

Per PROJECT_OPERATING_MODEL.md, always work in this order:

```
1. Core mechanics (shooting, scoring)  → COMPLETE ✓
       ↓
2. Server security (validation, anti-cheat) → COMPLETE ✓
       ↓
3. Data persistence (DataStore) → COMPLETE ✓
       ↓
4. Progression systems (XP, levels) → COMPLETE ✓
       ↓
5. Monetization hooks → CURRENT
       ↓
6. UI polish (LAST) → Basic HUD done, progression UI pending
```

---

## Blockers

None currently. Phase 4 complete, ready for UI polish and monetization.

---

## Definition of Done (MVP)

1. [x] Player can join, hit target, earn score ✓
2. [x] Player can play Quick Match (round system with persistence) ✓
3. [x] XP, level, currency, and stats persist across sessions ✓
4. [x] Daily rewards work with streak tracking (server-side) ✓
5. [x] Leaderboards store top scores for daily/weekly/all-time ✓
6. [x] Zero critical errors in playtest output ✓
7. [ ] Daily reward UI allows claiming rewards
8. [ ] Leaderboard UI displays top 50 players
9. [ ] Shop allows cosmetic purchases

---

## Document History

| Date | Change |
|------|--------|
| 2026-03-25 | Initial NEXT_STEPS.md created |
| 2026-03-25 | Updated for Phase 2 completion, Phase 3 priorities |
| 2026-03-26 | Phase 3 & 4 complete, updated for Phase 5 (Monetization/UI) |
