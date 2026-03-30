# Village + Trails World Redesign Spec

## Purpose
Replace the flat 150-stud disc hub with a medieval village connected by themed trails to each range. Players discover ranges through exploration, not line-of-sight. Each trail has its own biome from the first step out of the village. Locked ranges end with grand mural artwork on gates.

## Village Square (~60 stud area, center)

### Layout
- Spawn at fountain center (0, 2, -35)
- Irregular organic shape (not a perfect circle) — cobblestone with grass edges
- Surrounded by low stone walls and hedges (blocks sightlines to trails)

### Features (centralized)
- Marble fountain (landmark)
- Market stalls (3 shops, clustered near fountain)
- Game Pass display boards (near market)
- Daily Spin Wheel (near fountain)
- Winners Podium (in the square)
- Campfire (edge of square, gateway to social)
- 6 directional signposts (one per trail entrance)

### Features NOT in village (moved to trails)
- Tavern ("The Archer's Rest") → moved to Greenwood trail midpoint
- Outfitter ("The Outfitter") → moved to Castle trail start
- Carousel → moved to trail crossroads area
- VIP Lounge → moved to Sky Temple trail
- Trampolines → 2 per trail (Greenwood + Castle), discovery moments

## Trail System (6 trails, 100-150 studs each)

### Design Rules
1. Each trail has its own biome FROM THE FIRST STEP — no shared generic forest
2. Trails curve and use terrain elevation to block line-of-sight to other trails and ranges
3. Landmark every ~30 studs (shop, prop cluster, particle effect, or terrain feature)
4. Path material changes progressively (cobblestone → trail-specific material)
5. Trail width: 5-6 studs, with themed borders

### Trail 1: Greenwood (North) — OPEN
- **Length:** 120 studs
- **Biome:** Lush forest, getting denser
- **Path:** Cobblestone → dirt → mossy dirt
- **Props:** Mushroom clusters, fallen logs, fern patches, stream crossing (small bridge), bird particle effects
- **Landmark:** Tavern at ~60 studs (midway rest stop)
- **Trampolines:** 2, placed at ~30 and ~90 studs
- **Arrival:** Ranger Outpost — wooden stockade gate, supply crates, bonfire, shooting lane beyond
- **Terrain:** Flat → slight uphill → levels off at clearing

### Trail 2: Castle (East) — OPEN (Level 5)
- **Length:** 130 studs
- **Biome:** Medieval stonework, getting grander
- **Path:** Cobblestone → flagstone → polished stone
- **Props:** Stone walls rising along sides, iron lanterns on posts, heraldic banners, guard statues (2)
- **Landmark:** Outfitter at ~40 studs (fits medieval theme)
- **Trampolines:** 2, placed at ~50 and ~100 studs
- **Arrival:** Castle corridor → enclosed stone hall with throne target
- **Terrain:** Flat → gradual ascent (approaching the castle on a hill)

### Trail 3: Ember Depths (Southwest) — LOCKED
- **Length:** 100 studs
- **Biome:** Volcanic, hostile, hot
- **Path:** Cobblestone → cracked obsidian → glowing volcanic rock
- **Props:** Lava fissures (Neon orange strips in ground), charred tree stumps, smoke particles, ember emitters, heat shimmer (distortion effect placeholder)
- **Landmarks:** Volcanic boulder cluster at ~40 studs, lava pool at ~70 studs
- **Arrival:** Massive basalt gate with GRAND MURAL (SurfaceGui showing volcanic forge interior with molten lava rivers and obsidian archery range)
- **Terrain:** Flat → descending into a ravine (going down into the depths)

### Trail 4: Crystal Caverns (Northwest) — LOCKED
- **Length:** 100 studs
- **Biome:** Frozen, crystalline, ethereal
- **Path:** Cobblestone → frost stone → ice
- **Props:** Ice crystal formations (Glass wedges), frozen puddles (flat glass parts), icicle stalactites on overhead arches, snowfall particle emitters, frost mist at ground level
- **Landmarks:** Frozen waterfall at ~50 studs, crystal arch at ~80 studs
- **Arrival:** Glacier gate with GRAND MURAL (ice palace interior with frozen target and aurora borealis ceiling)
- **Terrain:** Flat → descending into a cavern mouth (entering underground)

### Trail 5: Sky Temple (Southeast) — LOCKED
- **Length:** 110 studs
- **Biome:** Celestial, divine, golden
- **Path:** Cobblestone → white marble → golden tiles
- **Props:** Floating lanterns (anchored glowing orbs), cloud wisps (low-transparency white parts), golden vine reliefs on path borders, wind chime parts, feather particles
- **Landmarks:** VIP Lounge at ~40 studs (red carpet + gold, fits divine theme), marble meditation circle at ~80 studs
- **Arrival:** Marble gate with GRAND MURAL (floating temple among clouds with golden archery range and divine light beams)
- **Terrain:** Ascending uphill (climbing toward the sky)

### Trail 6: The Deep (South) — LOCKED
- **Length:** 100 studs
- **Biome:** Aquatic, mysterious, deep ocean
- **Path:** Cobblestone → wet stone (darker slate) → coral-encrusted stone
- **Props:** Tide pools (small glass water patches), shells and barnacles on path borders, seaweed strands hanging from overhead arches, water drip particles, bioluminescent mushrooms (Neon cyan small parts), coral formations
- **Landmarks:** Shipwreck bow (half-buried ship hull at ~50 studs), octopus statue at ~80 studs
- **Arrival:** Coral-encrusted gate with octopus + GRAND MURAL (deep ocean abyss range with sunken ship targets and bioluminescent lighting)
- **Terrain:** Descending (going deeper underwater)

## Terrain & Sightline Design

### Elevation Map
- Village: Y = 2 (ground level)
- Greenwood: Y = 2 → 4 → 2 (over a gentle hill)
- Castle: Y = 2 → 5 (uphill to castle)
- Ember: Y = 2 → -2 (descending into ravine)
- Crystal: Y = 2 → -1 (descending into cavern)
- Sky: Y = 2 → 8 (ascending to temple)
- Deep: Y = 2 → -3 (descending to depths)

### Sightline Blockers
- Terrain hills between trails (3-5 stud rises)
- Dense vegetation walls at trail entrances
- Stone walls / hedge rows around village perimeter
- Each trail entrance is a narrow gap in the village boundary

## Grand Murals (Locked Gates)

### Implementation
- Large Part (12x8 studs) on gate wall face
- SurfaceGui with CanvasSize 1200x800
- Background: gradient matching range theme
- Foreground: Text labels creating scene description + symbolic imagery
- Since we can't upload images, use:
  - Colored Frames as compositional elements
  - TextLabels for decorative text ("EMBER DEPTHS" in flame font)
  - UIGradient for atmospheric color washes
  - Layered frames creating a stylized scene

### Mural Content
- **Ember Depths:** Dark-to-orange gradient, flame border, "FORGED IN FIRE" text, orange glow center
- **Crystal Caverns:** Blue-to-white gradient, crystal border shapes, "FROZEN IN TIME" text, blue glow
- **Sky Temple:** Gold-to-white gradient, sun ray lines, "ABOVE THE CLOUDS" text, golden glow
- **The Deep:** Teal-to-black gradient, tentacle border shapes, "WHAT LURKS BELOW" text, cyan glow

## What Gets Demolished
- The 150-stud cylinder hub platform
- Hub rim
- All radial pathways
- All flower beds
- All lamp posts along ring path
- All benches along ring path
- Current gate positions (rebuilt at trail ends)

## What Gets Preserved
- All 6 range gates (moved to trail endpoints)
- Gate wall decorations (lava cracks, crystals, golden vines, octopus)
- Gate particles and effects
- Fountain (stays in village)
- Campfire (stays in village)
- Market stalls (stay in village)
- Podium (stays in village)
- Spin wheel (stays in village)
- Game Pass boards (stay in village)
- All range interiors (Greenwood, Castle — untouched)

## What Gets Relocated
- Tavern → Greenwood trail midpoint
- Outfitter → Castle trail start
- Carousel → trail crossroads area
- VIP Lounge → Sky Temple trail
- Trampolines → distributed along open trails (2 each)

## Execution Order
1. Save current gate positions/decorations
2. Demolish flat disc platform
3. Build village square (smaller, organic)
4. Build terrain elevation around village (sightline blockers)
5. Build Trail 1: Greenwood (open, critical path)
6. Build Trail 2: Castle (open, critical path)
7. Build Trail 3-6: Locked trails (themed, shorter)
8. Create grand murals on locked gates
9. Relocate shops to trail positions
10. Playtest: walk each trail, verify sightlines blocked, verify range access

## Success Criteria
- Standing in the village square, ZERO ranges are visible
- Each trail feels like a unique biome from step one
- Walking a trail takes 10-15 seconds
- Locked gates show beautiful grand murals, not blank walls
- No two trails share props or materials
- The world feels like an adventure, not a lobby
