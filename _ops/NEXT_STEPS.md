# Archery Legends Next Steps

**Last Updated:** 2026-03-28
**Current Phase:** Range Polish & Gameplay Feedback

---

## In Progress: Phase 2 — Client Gameplay Feedback (7 items)

### C1. HUD Countdown Display
- [ ] Listen for RoundCountdown remote
- [ ] Center-screen "3→2→1→FIRE!" with scale tween + fade
- [ ] 72px GothamBlack, white numbers, green "FIRE!"

### C2. 3D Score Popup at Impact
- [ ] BillboardGui at hitPosition from ArrowResult
- [ ] Zone-colored "+10 BULLSEYE!" text, rises 3 studs, fades

### C3. Impact Particle Burst
- [ ] Emit(20) particles at hitPosition, zone-colored
- [ ] PointLight flash 0.3s, auto-destroy

### C4. Camera Shake on Bullseye
- [ ] Micro shake 0.2s on zone=="Bullseye" only

### C5. Near-Miss Indicator
- [ ] "MISS — X studs away!" when distanceFromCenter < Edge+2

### C6. Streak Counter
- [ ] "STREAK x3!" on consecutive hits, breaks on miss

### C7. Arrow Count Pulse
- [ ] Red pulse when arrows ≤ 3, "FINAL ARROW" on last

---

## Upcoming: Phase 3 — Greenwood Visual Polish (10 items)
- [ ] Hay bales flanking target
- [ ] Range distance markers (10m-40m)
- [ ] Wind flag on archway
- [ ] Quiver stand + scoreboard + bench on deck
- [ ] Tree line replenishment (20 trees along lane)
- [ ] Ground flowers along path
- [ ] Target backstop (earth mound)
- [ ] Fence posts along lane edges

## Upcoming: Phase 4 — Castle Visual Polish (10 items)
- [ ] Throne steps + rug widening
- [ ] Throne room banners (crown + crossed swords)
- [ ] Weapon racks between armored suits
- [ ] Stained glass windows (6, colored PointLights)
- [ ] Dust particle atmosphere
- [ ] Corridor stone arches + torch brackets
- [ ] Wall sconces between tapestries
- [ ] Crown sparkle particle effect

---

## Completed This Session

| Task | Status |
|------|--------|
| Phase 1: Server mechanics (countdown, arrow stick, distanceFromCenter) | DONE |
| Hub cleanup (108 trees removed, pathways, lamps, benches, flowers) | DONE |
| Gate wall decorations (4 themed gates) | DONE |
| "Sunken Sanctum" renamed to "The Deep" + full octopus | DONE |
| Grass ground removed, proper ground planes added | DONE |
| HUD initial mode bug fixed (hudMode="init") | DONE |

---

## Document History

| Date | Change |
|------|--------|
| 2026-03-25 | Initial |
| 2026-03-26 | Phase 6 complete |
| 2026-03-27 | Environment, sounds, UI polish |
| 2026-03-28 | Hub + Castle + HUD + server mechanics + hub cleanup + gate decoration |
