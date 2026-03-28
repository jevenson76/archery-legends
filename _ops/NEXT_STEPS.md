# Archery Legends Next Steps

**Last Updated:** 2026-03-28
**Current Phase:** Post-MVP — Final Polish & Pre-Publish

---

## Immediate Priority

### 1. Gameplay Testing & Tuning
- [ ] Playtest full round: draw → fire → hit detection → score → round end
- [ ] Verify HUD shows during gameplay (score, arrows, XP bar, streak)
- [ ] Tune accuracy spread values (BaseSpread=0.04 may need adjustment)
- [ ] Verify arrow flight arc looks natural at 50-stud range
- [ ] Test bow release sound (twang) feels right

### 2. Environment Polish
- [ ] Add grass/bush details along path borders
- [ ] Add book stand / sign at shooting deck (per concept art)
- [ ] Consider side targets visible from lane
- [ ] Verify extended lane looks good with longer torch rows

---

## Pre-Publish Checklist
- [ ] Replace Game Pass placeholder IDs (currently 0)
- [ ] Enable "Studio Access to API Services" for DataStore testing
- [ ] Final zero-error playtest with DataStore enabled
- [x] Mobile viewport verification (scale-based panels + UISizeConstraint)
- [ ] Upload custom bow draw/release audio for better quality
- [ ] Set game icon and thumbnails
- [ ] Test on mobile device

---

## Known Issues
- Screenshot MCP tool times out (known Roblox Studio bug)
- Some marketplace audio assets are longer than ideal (bullseye bell 2.8s, miss whoosh 3.1s) — custom uploads would be shorter
- HitInner and HitOuter share same thud asset (differentiated by PlaybackSpeed only)

---

## Completed (This Session — 2026-03-28)

| Task | Status |
|------|--------|
| Fixed bullseye detection (was broken — all shots were MISS) | DONE |
| Fixed HUD invisible (StarterGui folder conflicts) | DONE |
| Fixed platform not visible (raised + thickened deck) | DONE |
| Fixed target off-center (X=3 → X=0) | DONE |
| Fixed mountain blocking view (Z=-0.7 → Z=130) | DONE |
| Rebuilt missing TargetArchway with sign | DONE |
| Added accuracy spread system (server-side) | DONE |
| Added client-side arrow flight animation | DONE |
| Arrow trail matches equipped shop trail | DONE |
| Extended lane from 26 to 50 studs | DONE |
| Fixed bow release sound (sword → twang) | DONE |
| Replaced 6 mismatched audio assets | DONE |
| Fixed BowDraw stop-on-release (was 6.6s runaway) | DONE |

## Completed (Previous Session — 2026-03-27)

| Task | Status |
|------|--------|
| UI Polish Pass (green theme, consistency, mobile) | DONE |
| Sound integration (SoundManager, 16 sounds wired) | DONE |
| Environment overhaul (concept art match) | DONE |
| World bow (welded to hand) | DONE |
| Sound asset tuning (Volume/PlaybackSpeed) | DONE |

---

## Previously Completed Phases

- Phase 1: Foundation (arena, target, config, types, remotes)
- Phase 2: Core Mechanic (bow, arrows, hit detection, rounds)
- Phase 3: Data Persistence (DataStore, XP/currency)
- Phase 4: Progression (XP bar, daily rewards, leaderboards)
- Phase 5: Monetization/UI (shop, daily reward UI, leaderboard UI)
- Phase 6: Game Modes (Quick Match, Practice, Duel, Game Passes)

---

## Document History

| Date | Change |
|------|--------|
| 2026-03-25 | Initial NEXT_STEPS.md |
| 2026-03-26 | Phase 6 complete, AAA visual overhaul 9/10 done |
| 2026-03-27 | Environment overhaul, sounds, UI polish complete |
| 2026-03-28 | Gameplay fixes, accuracy system, arrow flight, lane extension |
