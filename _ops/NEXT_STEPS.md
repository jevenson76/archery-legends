# Archery Legends Next Steps

**Last Updated:** 2026-03-27
**Current Phase:** Post-MVP — AAA Visual Overhaul

---

## Immediate Priority

### 1. First-Person Bow (Part 6 of 10-part overhaul) — DESIGN APPROVED

Add visible bow model during gameplay using ViewportFrame in BowController.

**Approach:** ViewportFrame + detailed 8-10 part model, built into BowController.

**Deliverables:**
- [ ] ViewportFrame in BowUI ScreenGui (bottom-center, 30%x40%)
- [ ] Detailed bow model: ornate limbs with grain, wrapped grip, visible string (Beam), nocked arrow with fletching
- [ ] Camera angle for first-person perspective
- [ ] Draw animation (string pulls back proportional to `currentPower`)
- [ ] Skin recoloring from Config.ShopItems.BowSkins Color property
- [ ] Trail effect on nocked arrow when equipped

**Resume point:** Design decided, ready to implement. User chose option B (detailed/ornate).

### 2. UI Polish Pass
- [ ] Fine-tune button order (STORE, LEADERBOARD, PRACTICE)
- [ ] Style Find Duel button to match green theme
- [ ] Test all popups (shop, leaderboard, daily rewards) with new button wiring
- [ ] Mobile viewport testing

### 3. Sound Assets
- [ ] Replace placeholder `rbxassetid://0` with real Roblox Audio Library assets
- [ ] 16 punchy sounds per audio design doc

---

## Completed (This Session)

### 10-Part AAA Visual Overhaul (9/10 complete)

| Part | Status | Description |
|------|--------|-------------|
| 1. Ground | DONE | Green grass material |
| 2. Banner | DONE | Wooden gate archway + "Archery Legends" sign |
| 3. HUD | DONE | Full info panel (streak, score, level, arrows, arrow type) |
| 4. Range Data | DONE | Bottom-right panel (distance, wind) |
| 5. Buttons | DONE | Icon+text labels (STORE, LEADERBOARD, PRACTICE) |
| 6. First-Person Bow | PENDING | ViewportFrame bow model |
| 7. Forest | DONE | 179 trees + 40 bushes, varied heights |
| 8. Lake | DONE | Large lake with dock, lily pads |
| 9. Lane Fencing | DONE | Split-rail wooden fence |
| 10. Atmosphere | DONE | Golden hour, campfire, haze, bloom, sun rays |

### Key fixes:
- Target glow removed (8 SurfaceLights + 1 SpotLight)
- Banner SurfaceGui face corrected (Front, not Back)
- HUDButtonBar refactored to callback-only registry
- MCP stale process cleanup documented

---

## Previously Completed Phases

- Phase 1: Foundation (arena, target, config, types, remotes)
- Phase 2: Core Mechanic (bow, arrows, hit detection, rounds)
- Phase 3: Data Persistence (DataStore, XP/currency)
- Phase 4: Progression (XP bar, daily rewards, leaderboards)
- Phase 5: Monetization/UI (shop, daily reward UI, leaderboard UI)
- Phase 6: Game Modes (Quick Match, Practice, Duel, Game Passes)

---

## Pre-Publish Checklist
- [ ] Replace Game Pass placeholder IDs (currently 0)
- [ ] Enable "Studio Access to API Services" for DataStore
- [ ] Final zero-error playtest
- [ ] Mobile viewport verification

---

## Document History

| Date | Change |
|------|--------|
| 2026-03-25 | Initial NEXT_STEPS.md |
| 2026-03-26 | Phase 6 complete, AAA visual overhaul 9/10 done |
| 2026-03-27 | First-person bow design approved, ready to implement |
