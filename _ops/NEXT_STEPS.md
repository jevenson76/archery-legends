# Archery Legends Next Steps

**Last Updated:** 2026-03-26
**Current Phase:** MVP — Phase 6: Game Modes & Game Passes

---

## Immediate Priority

### 1. 1v1 Duel Mode

Create competitive multiplayer mode:

**Deliverables:**
- [ ] DuelManager.server.luau for matchmaking
- [ ] Alternating turns (5 arrows each)
- [ ] Side-by-side dual targets
- [ ] Real-time score comparison
- [ ] Winner/loser results screen

### 2. Game Passes (MarketplaceService)

Implement premium monetization:

**Deliverables:**
- [ ] VIP Pass: 2x XP + chat tag
- [ ] Double Currency Pass
- [ ] Radio Pass: play custom audio
- [ ] ProcessReceipt handling with idempotency

### 3. Practice Mode

Unlimited training mode:

**Deliverables:**
- [ ] No arrow limit
- [ ] No score persistence
- [ ] "Practice" indicator in HUD
- [ ] Quick exit to ranked play

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

### Phase 5: Monetization / UI Polish ✓

| Task | Status |
|------|--------|
| Daily Reward UI (7-day calendar, claim popup) | ✓ |
| Leaderboard UI (tabs, top 50, auto-refresh) | ✓ |
| ShopManager (purchase processing, ownership) | ✓ |
| ShopController (bow skins, arrow trails) | ✓ |
| Config.ShopItems catalog | ✓ |
| Types.OwnedItems field | ✓ |

---

## Pending Implementation (per mvp-task-list.md)

### Phase 6: Game Modes (Days 15-16)

| Task | Status | Reference |
|------|--------|-----------|
| 1v1 Duel Mode | PENDING | Day 15-16 |
| Practice Mode | PENDING | Day 16 |
| Game Passes | PENDING | Day 12 |

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
5. Monetization hooks → COMPLETE ✓ (Shop, currency system)
       ↓
6. UI polish → COMPLETE ✓ (Daily rewards, leaderboard, shop UI)
       ↓
7. Game modes → CURRENT (Duel, Practice, Game Passes)
```

---

## Blockers

None currently. Phase 5 complete, ready for game modes.

---

## Definition of Done (MVP)

1. [x] Player can join, hit target, earn score ✓
2. [x] Player can play Quick Match (round system with persistence) ✓
3. [x] XP, level, currency, and stats persist across sessions ✓
4. [x] Daily rewards work with streak tracking (server-side) ✓
5. [x] Leaderboards store top scores for daily/weekly/all-time ✓
6. [x] Zero critical errors in playtest output ✓
7. [x] Daily reward UI allows claiming rewards ✓
8. [x] Leaderboard UI displays top 50 players ✓
9. [x] Shop allows cosmetic purchases ✓
10. [ ] 1v1 Duel mode allows competitive play
11. [ ] Game Passes grant premium benefits

---

## Document History

| Date | Change |
|------|--------|
| 2026-03-25 | Initial NEXT_STEPS.md created |
| 2026-03-25 | Updated for Phase 2 completion, Phase 3 priorities |
| 2026-03-26 | Phase 3 & 4 complete, updated for Phase 5 (Monetization/UI) |
| 2026-03-26 | Phase 5 complete, updated for Phase 6 (Game Modes) |
