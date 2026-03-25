# Archery Legends Next Steps

**Last Updated:** 2026-03-25
**Current Phase:** MVP — Phase 3: Data Persistence

---

## Immediate Priority

### 1. DataStore Setup (Day 7)

Create `ServerScriptService/DataManager.server.luau`:

**Deliverables:**
- [ ] GetDataStore for player data
- [ ] Load player data on join (with retry logic)
- [ ] Default data initialization from Types.GetDefaultPlayerData()
- [ ] pcall wrapping for all DataStore operations

**MCP Workflow:**
```
create_object (Script) → set_script_source → start_playtest → verify loads
```

### 2. Auto-Save System (Day 8)

Extend DataManager with save logic:

**Deliverables:**
- [ ] Save on round end (via RoundEnd event)
- [ ] Save on player leaving (PlayerRemoving)
- [ ] Debounced saves (no more than 1 per 6 seconds)
- [ ] BindToClose for server shutdown saves

### 3. XP and Leveling

Connect scoring to progression:

**Deliverables:**
- [ ] Award XP based on score (from Config.PROGRESSION.XP_PER_POINT)
- [ ] Level up detection with reward grants
- [ ] Update HUD to show XP bar and level

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

---

## Pending Implementation (per mvp-task-list.md)

### Phase 3: Data Persistence (Days 7-8)

| Task | Status | Reference |
|------|--------|-----------|
| DataStore Setup | PENDING | Day 7 |
| Auto-Save & Session Persistence | PENDING | Day 8 |

### Phase 4: Progression (Days 9-10)

| Task | Status | Reference |
|------|--------|-----------|
| XP & Level System | PENDING | Day 9 |
| Currency & Unlocks | PENDING | Day 10 |

### Phase 5-7: See mvp-task-list.md

Full 20-day plan in `docs/mvp-task-list.md`

---

## Work Order Reminder

Per PROJECT_OPERATING_MODEL.md, always work in this order:

```
1. Core mechanics (shooting, scoring)  → COMPLETE ✓
       ↓
2. Server security (validation, anti-cheat) → COMPLETE ✓
       ↓
3. Data persistence (DataStore) → CURRENT
       ↓
4. Progression systems (XP, levels) → PENDING
       ↓
5. Monetization hooks → DEFERRED (post-MVP)
       ↓
6. UI polish (LAST) → Basic HUD done, polish pending
```

---

## Blockers

None currently. Phase 2 complete, ready for DataStore integration.

---

## Definition of Done (MVP)

1. [x] Player can join, hit target, earn score ✓
2. [ ] Player can play Quick Match (round system in place, needs persistence)
3. [ ] XP, level, currency, and stats persist across sessions
4. [ ] Daily rewards work with streak tracking
5. [ ] Leaderboards display top 50 for daily/weekly/all-time
6. [x] Zero critical errors in playtest output ✓

---

## Document History

| Date | Change |
|------|--------|
| 2026-03-25 | Initial NEXT_STEPS.md created |
| 2026-03-25 | Updated for Phase 2 completion, Phase 3 priorities |
