# Archery Legends Next Steps

**Last Updated:** 2026-03-25
**Current Phase:** MVP — Phase 2: Core Mechanic

---

## Immediate Priority

### 1. BowController — Input & Aim (Day 3)

Create `StarterPlayerScripts/BowController.client.luau`:

**Deliverables:**
- [ ] Mouse aim tracking (bow follows cursor direction)
- [ ] Draw mechanic (hold LMB to charge power 0-100% over 1.5s)
- [ ] Power meter UI visualization
- [ ] Aim arc trajectory preview (using Config gravity value)
- [ ] Release fires (log for now, no server communication yet)

**MCP Workflow:**
```
create_object (LocalScript) → set_script_source → start_playtest → verify input
```

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

---

## Pending Implementation (per mvp-task-list.md)

### Phase 2: Core Mechanic (Days 3-6)

| Task | Status | Reference |
|------|--------|-----------|
| Bow Controller — Input & Aim | PENDING | Day 3 |
| Arrow Flight & Server Communication | PENDING | Day 4 |
| Hit Detection & Scoring | PENDING | Day 5 |
| Quick Match Round Logic | PENDING | Day 6 |

### Phase 3: Data Persistence (Days 7-8)

| Task | Status | Reference |
|------|--------|-----------|
| DataStore Setup | PENDING | Day 7 |
| Auto-Save & Session Persistence | PENDING | Day 8 |

### Phase 4-7: See mvp-task-list.md

Full 20-day plan in `docs/mvp-task-list.md`

---

## Work Order Reminder

Per PROJECT_OPERATING_MODEL.md, always work in this order:

```
1. Core mechanics (shooting, scoring)  → PENDING
       ↓
2. Server security (validation, anti-cheat) → PENDING
       ↓
3. Data persistence (DataStore) → PENDING
       ↓
4. Progression systems (XP, levels) → PENDING
       ↓
5. Monetization hooks → DEFERRED (post-MVP)
       ↓
6. UI polish (LAST) → PENDING
```

---

## Blockers

None currently. MCP connection verified, foundation complete.

---

## Definition of Done (MVP)

1. [ ] Player can join, see tutorial, hit target, earn score
2. [ ] Player can play Quick Match and 1v1 Duel
3. [ ] XP, level, currency, and stats persist across sessions
4. [ ] Daily rewards work with streak tracking
5. [ ] Leaderboards display top 50 for daily/weekly/all-time
6. [ ] Zero critical errors in playtest output

---

## Document History

| Date | Change |
|------|--------|
| 2026-03-25 | Initial NEXT_STEPS.md created |
