# Archery Legends Next Steps

**Last Updated:** 2026-03-28
**Current Phase:** Post-MVP — Pre-Publish Polish

---

## Immediate Priority

### 1. Full Gameplay Testing
- [ ] Walk hub → Greenwood → shoot 10 arrows → verify scoring + round end
- [ ] Walk hub → Castle → shoot at throne → verify scoring works
- [ ] Verify HUD transitions (hub compact → range full → hub compact)
- [ ] Test arrow flight animation (visible arc from bow to target)
- [ ] Test bow draw/release sounds
- [ ] Verify accuracy spread feels right (tune BaseSpread if needed)

### 2. Character Skin System Backend
- [ ] Implement outfit application (Shirt + Pants textures on character)
- [ ] Wire "The Outfitter" shop mannequins to purchase/equip flow
- [ ] Add character skin data to PlayerData/DataStore schema

### 3. Environment Polish
- [ ] Add grass/bush details along hub paths
- [ ] Refine castle corridor (currently bare walls)
- [ ] Add ambient sounds per zone (forest birds for Greenwood, echoes for Castle)

---

## Pre-Publish Checklist
- [ ] Replace Game Pass placeholder IDs (currently 0)
- [ ] Enable "Studio Access to API Services" for DataStore testing
- [ ] Final zero-error playtest with DataStore enabled
- [x] Mobile viewport verification (scale-based panels + UISizeConstraint)
- [ ] Upload custom bow draw/release audio for better quality
- [ ] Set game icon and thumbnails
- [ ] Test on mobile device
- [ ] Level 5 gate check for Castle Range entrance

---

## Future Content (Post-Launch)
- [ ] Build Castle Range interior details (more furniture, throne room details)
- [ ] Build first locked range when ready (Ember Depths or Crystal Caverns)
- [ ] Daily Spin Wheel functionality (backend)
- [ ] Character skin system (applying outfits)
- [ ] Battle Pass system
- [ ] Tournament mode
- [ ] Clan system

---

## Document History

| Date | Change |
|------|--------|
| 2026-03-25 | Initial NEXT_STEPS.md |
| 2026-03-26 | Phase 6 complete, AAA visual overhaul |
| 2026-03-27 | Environment overhaul, sounds, UI polish |
| 2026-03-28 | Hub + Castle + multi-target + context-sensitive HUD |
