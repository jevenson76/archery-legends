# Archery Legends Next Steps

**Last Updated:** 2026-03-25
**Current Phase:** MVP — Phase 1: Foundation

---

## Immediate Priority

### 1. Verify Roblox Studio Connection (Required First)

Before proceeding with any development, verify MCP connection:

```
Use MCP tool: get_place_info
```

**If connection fails:**
- Verify Roblox Studio is running
- Verify robloxstudio-mcp plugin is installed
- Check MCP server status

**Blocker:** Cannot proceed with development until Studio connection verified.

---

## Pending Implementation (per mvp-task-list.md)

### Phase 1: Foundation (Days 1-2)

| Task | Status | Reference |
|------|--------|-----------|
| Arena & Project Structure | PENDING | mvp-task-list.md Day 1 |
| Config Module & Remotes | PENDING | mvp-task-list.md Day 2 |

**Day 1 Deliverables:**
- [ ] Flat arena ground plane (100x100 studs)
- [ ] Firing line position marker
- [ ] Target stand at 30 studs distance
- [ ] Target model with 4 concentric zones
- [ ] SpawnLocation at firing line
- [ ] Complete folder structure

**Day 2 Deliverables:**
- [ ] `ReplicatedStorage/Modules/Config.luau`
- [ ] `ReplicatedStorage/Remotes/` with all RemoteEvents/Functions
- [ ] `ReplicatedStorage/Modules/Types.luau`

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

| Blocker | Impact | Resolution |
|---------|--------|------------|
| Studio connection unverified | Cannot develop | Run get_place_info via MCP |
| No Studio project created | Cannot develop | Create new Roblox place |

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
