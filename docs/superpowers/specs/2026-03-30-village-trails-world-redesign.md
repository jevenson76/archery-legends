# Village + Trails World Redesign Spec (v2 — Post-Critic)

## Purpose
EXTEND the existing hub with themed trail entrances that block sightlines to ranges. Players discover ranges through exploration. Each trail has its own biome from the first step. Locked ranges end with stylized themed posters on gates.

## Critic Issues Addressed
1. **No demolition** — keep existing hub platform, add trail extensions from perimeter
2. **Sightline blocking** — use 15-20 stud tall prop walls (dense tree walls, rock formations) at trail entrances, not terrain elevation
3. **Respawn** — add SpawnLocations in each range + teleport-back logic in GameManager
4. **Part count** — target max 400 new parts total, use LOD-friendly large simple shapes
5. **Murals** — realistic "themed poster" with UIGradient, not fake artwork
6. **Phased scope** — Phase 1: open trails (Greenwood + Castle). Phase 2: locked trails (4)
7. **Carousel location** — placed at village south edge near locked trail entrances

---

## Phase 1: Open Trail Extensions (THIS SESSION)

### What Changes
- Add **trail tunnels** at hub perimeter: dense prop walls forming a narrow corridor that blocks sightlines
- Extend paths from hub edge to existing range entrances with biome-appropriate props
- Relocate Tavern to Greenwood trail, Outfitter to Castle trail
- Add range SpawnLocations for respawn handling

### Trail 1: Greenwood Extension (North)
- **Length:** ~80 studs from hub rim to existing shooting deck
- **Sightline blocker:** Dense tree wall (20-stud tall, 30-stud wide) at hub exit — a wall of foliage players walk through a gap in
- **Path:** Existing cobblestone transitions to dirt (Mud material)
- **Props (budget: 60 parts):**
  - 8 large trees flanking path (already have tree pattern)
  - 6 fern/bush clusters (3 small green parts each = 18 parts)
  - 2 fallen logs across path (must step over)
  - 1 small stream crossing (Glass part + bridge)
  - Tavern relocated to midpoint
- **SpawnLocation:** On shooting deck, transparent, named "GreenwoodSpawn"

### Trail 2: Castle Extension (East)
- **Length:** ~90 studs from hub rim to existing corridor
- **Sightline blocker:** Stone wall section (20-stud tall, 30-stud wide) with narrow gate entrance
- **Path:** Cobblestone transitions to flagstone (Slate material)
- **Props (budget: 50 parts):**
  - 4 stone wall sections rising along path
  - 6 iron lanterns on posts
  - 2 heraldic banners
  - 2 guard statues (simplified: pedestal + body + helmet = 6 parts each)
  - Outfitter relocated to trail start
- **SpawnLocation:** On castle shooting platform, transparent

### Respawn Handling
- Add transparent SpawnLocation in each active range
- Modify GameManager: if player dies during round, respawn at range spawn, not hub
- Use `player.RespawnLocation` property set when entering a range zone
- Reset to hub spawn when returning to village

---

## Phase 2: Locked Trail Extensions (NEXT SESSION)

### Trail 3-6: Themed Dead-End Paths
- **Length:** 60-80 studs each (shorter — they're dead ends)
- **Budget:** 30-40 parts per trail (120-160 total)
- Each trail's biome starts immediately at hub exit
- Ends at existing decorated gate wall
- Gate wall gets a **themed poster** (SurfaceGui with UIGradient + styled text + colored frames)

### Trail 3: Ember Depths
- Path: cracked obsidian parts, 4 lava fissure strips (Neon orange), 3 charred stumps
- Existing gate decorations (lava cracks, embers) stay

### Trail 4: Crystal Caverns
- Path: frost stone, 4 ice crystal formations, frozen puddle parts
- Existing gate decorations (frost, crystals) stay

### Trail 5: Sky Temple
- Path: marble tiles, 4 floating golden orbs, cloud wisp parts
- VIP Lounge relocated here (fits divine/exclusive theme)
- Existing gate decorations (golden vines, clouds) stay

### Trail 6: The Deep
- Path: wet slate, 4 coral formations, seaweed strands, bioluminescent parts
- Existing gate decorations (octopus, drip) stay

---

## Part Budget

| Component | New Parts | Notes |
|-----------|-----------|-------|
| Greenwood trail props | ~60 | Trees, ferns, stream, logs |
| Castle trail props | ~50 | Walls, lanterns, banners, statues |
| Sightline blockers (2) | ~30 | Dense tree/stone walls at hub exits |
| Trail paths (2) | ~20 | Path material segments |
| Range SpawnLocations | 2 | Transparent, functional only |
| **Phase 1 Total** | **~162** | Well within budget |
| Phase 2 (4 locked trails) | ~140 | Next session |
| **Grand Total** | **~302** | Under 400 target |

## What Does NOT Change
- Hub platform stays (150-stud disc)
- All hub features stay in place (fountain, campfire, podium, market, spin wheel, game pass boards)
- All gate wall decorations stay
- All range interiors stay (Greenwood, Castle)
- Hub pathways stay (radial paths, ring path)
- Lamp posts, benches, flowers stay

## What Moves
- Tavern → Greenwood trail midpoint
- Outfitter → Castle trail start
- Carousel → village south edge (near locked trail entrances)

## Execution Order (Phase 1)
1. Build Greenwood sightline blocker (tree wall at hub north rim)
2. Build Greenwood trail path + props (80 studs)
3. Relocate Tavern to trail midpoint
4. Build Castle sightline blocker (stone wall at hub east rim)
5. Build Castle trail path + props (90 studs)
6. Relocate Outfitter to trail start
7. Add range SpawnLocations + respawn logic
8. Playtest: walk village → Greenwood, verify sightlines blocked
9. Playtest: walk village → Castle, verify sightlines blocked

## Success Criteria
- Standing in village center, neither range is visible (blocked by prop walls)
- Greenwood trail feels progressively greener/wilder
- Castle trail feels progressively more medieval/grand
- Dying in range respawns at range spawn, not village
- Total new parts < 200
- Zero runtime errors
