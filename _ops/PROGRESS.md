# Archery Legends Progress Log

**Last Updated:** 2026-03-31
**Project:** Archery Legends (Roblox Archery Game)
**Phase:** Post-MVP — Village Trails & World Polish

---

## Current State

| Asset | Status | Notes |
|-------|--------|-------|
| Design Documents | COMPLETE | GDD, engagement psychology, MVP task list |
| Operational Structure | COMPLETE | _ops/, .claude/commands/ mirroring ATL |
| **Phase 1: Foundation** | **COMPLETE** | Arena, target, folders, Config, Types, Remotes |
| **Arena Visual Polish** | **COMPLETE** | Terrain, particles, torches, lighting, target glow |
| **Phase 2: Core Mechanic** | **COMPLETE** | BowController, arrow flight, hit detection, round lifecycle |
| **UI/HUD** | **COMPLETE** | Score, arrows, hit feedback, round summary, XP/currency |
| **Phase 3: Data Persistence** | **COMPLETE** | DataManager, auto-save, XP/currency awards |
| **Phase 4: Progression** | **COMPLETE** | XP bar, daily rewards, leaderboards |
| **Phase 5: Monetization/UI** | **COMPLETE** | Daily Reward UI, Leaderboard UI, Shop system |
| **Phase 6: Game Modes** | **COMPLETE** | Quick Match, Practice, Duel, Game Passes |
| **World Bow** | **COMPLETE** | 3D bow welded to character left hand |
| **Environment Overhaul** | **COMPLETE** | Concept art-matched arena rebuild |
| **Sound Assets** | **COMPLETE** | 16 audio instances with real asset IDs |
| **HUD Reorder** | **COMPLETE** | Streak to bottom, hidden when 0 |
| **UI Polish Pass** | **COMPLETE** | Green theme, consistency, mobile responsive |
| **Sound Integration** | **COMPLETE** | SoundManager module, all 16 sounds tuned + wired |
| **Accuracy System** | **COMPLETE** | Server-side spread, SteadyHand shop item, power scaling |
| **Gameplay Fixes** | **COMPLETE** | Platform, HUD, lane length, arrow flight, bullseye detection |
| **Community Hub** | **COMPLETE** | 150-stud courtyard, 6 range gates, crowd magnets, shops |
| **Castle Range** | **COMPLETE** | Enclosed stone hall, throne target, tapestries, armored suits |
| **Multi-Target Engine** | **COMPLETE** | GameManager ranges registry, position-based detection |
| **Context-Sensitive HUD** | **COMPLETE** | Hub mode (compact) vs Range mode (full), smooth tweens |
| **Hub Visual Cleanup** | **COMPLETE** | Trees cleared, pathways, lamps, benches, flowers, ground fixed |
| **Gate Wall Decorations** | **COMPLETE** | Ember/Crystal/Sky/Deep themed walls, octopus, particles |
| **Server Gameplay Mechanics** | **COMPLETE** | Countdown, arrow sticking, distanceFromCenter |
| **Client Gameplay Feedback** | **COMPLETE** | Countdown, popups, particles, shake, streak, near-miss, arrow pulse |
| **Greenwood Range Polish** | **COMPLETE** | Hay bales, markers, trees, flowers, backstop, fences |
| **Castle Range Polish** | **COMPLETE** | Steps, banners, weapons, glass, dust, arches, sconces, crown sparkle |
| **Character Skins** | **COMPLETE** | 6 skins in shop, body color applier, SKINS tab |
| **Daily Spin Wheel** | **COMPLETE** | SpinWheelController, animation, reward popup, confetti |
| **Village Trails Phase 1** | **COMPLETE** | Greenwood + Castle trail extensions, sightline blockers |
| **Rank-Based Matchmaking** | **COMPLETE** | ±1 tier matching, 15s expansion to ±2 tiers |

---

## Completed Work

### 2026-03-28: Server Gameplay Mechanics + Hub Cleanup (COMPLETE)

**Status:** COMPLETE

**Server Mechanics (GameManager):**
- Round countdown: 3→2→1→FIRE! via RoundCountdown RemoteEvent (0.8s per number)
- Arrows stick in target until round end (60s safety, cleanup via ShotBy attribute)
- distanceFromCenter added to SimulationResult + ArrowResult payloads (enables near-miss)
- Miss detection improved: arrows crossing target plane without scoring store distance

**Hub Visual Cleanup:**
- Removed 108 forest trees inside hub radius
- Removed arena_ground (grass plane blocking hub)
- Added Greenwood/Castle/backdrop/surround ground planes
- Added 6 radial cobblestone pathways, circular ring path (24 segments)
- Added 12 lamp posts, 6 benches, 12 flower beds
- Fixed HUD initial mode (hudMode="init" → first setHudMode applies)
- Removed duplicate Lake folder, empty Targets folder

**Gate Wall Decorations:**
- Ember Depths: basalt walls, 16 lava cracks, glow strips, flame banners
- Crystal Caverns: glacier walls, 12 crystal formations, frost strips, ice banners
- Sky Temple: marble walls, golden vine reliefs, cloud wisps, floating orbs, gold banners
- The Deep (renamed from Sunken Sanctum): teal slate walls, coral, seaweed, shells, full octopus with 6 tentacles + head + eyes

---

### 2026-03-28: Context-Sensitive HUD System (COMPLETE)

**Status:** COMPLETE

Added position-based HUD mode switching with smooth tween transitions.

| Feature | Details |
|---------|---------|
| Hub mode | Compact panel (75px): Level, XP bar, Currency, Streak only |
| Range mode | Full panel (160px): all gameplay elements visible |
| Range badge | Top-center badge showing "GREENWOOD RANGE" / "CASTLE RANGE" |
| Zone detection | Client-side position check with 5-stud hysteresis at 4Hz |
| Tween transitions | 0.3s Quad ease, tween cancellation on rapid switching |
| Gate prompts | ProximityPrompts on all 6 range gates |

**Critic fixes applied:** Synchronous gameplayRows collection (was task.defer race), tween cancellation (was stacking), getFirePosition forward reference (was nil call).

---

### 2026-03-28: Castle Range Build (COMPLETE)

**Status:** COMPLETE

Full Castle Range with GameManager multi-target refactor.

**GameManager Refactor:**
- Replaced single `target: Model?` with `ranges: {[string]: Model}` registry
- Added `detectPlayerRange(player)` — X > 50 = castle
- `simulateArrowFlight` now takes `rangeId` parameter
- Both targets registered on init

**Castle Interior (workspace.CastleRange):**
- 22x15x60 stud enclosed stone hall at X=85
- 8 marble columns, 4 vaulted arches, red carpet with gold borders
- Throne target at Z=45 (5 scoring rings matching Greenwood geometry)
- Gold crown as bullseye (smallest part detection)
- 6 heraldic tapestries (Lion, Eagle, Dragon, Stag, Crown, Shield)
- 6 armored suits with shields + swords
- 12 wall torches, 2 chandeliers, 2 throne spotlights
- Angled corridor connecting hub gate to hall entrance

---

### 2026-03-28: Community Hub & Multi-Zone Architecture (COMPLETE)

**Status:** COMPLETE

Built 150-stud hub-and-spoke courtyard with 6 range gates and crowd magnets.

**Hub Features:** Marble fountain, 4 trampolines, carousel (6 seats + lights), campfire (8 log seats), winners podium (G/S/B + spotlight), market stalls (3 shops), daily spin wheel, VIP lounge (red carpet + velvet ropes), Game Pass display boards, "The Archer's Rest" tavern (6 bow skin displays), "The Outfitter" character skin shop (6 mannequins + mirror).

**6 Range Gates:** Greenwood (open), Castle (open, Level 5), Ember Depths (locked, embers), Crystal Caverns (locked, frost), Sky Temple (locked, golden beams), Sunken Sanctum (locked, octopus tentacle).

---

### 2026-03-28: Gameplay Polish & Critical Bug Fixes (COMPLETE)

**Status:** COMPLETE

Major session fixing gameplay-breaking bugs and adding core mechanics.

**Critical Bug Fixes:**
| Fix | Details |
|-----|---------|
| Bullseye detection broken | GameManager looked for "New Yeller" color but target was "Deep orange". Changed to find smallest part (robust). Hits were ALL registering as MISS. |
| HUD invisible | 6 empty Folders in StarterGui conflicted with controller-created ScreenGuis. Deleted all placeholder folders. |
| Platform invisible | Shooting deck floor at Y=0.5 blended with ground. Raised deck 1 stud, thickened floor to 1.0 stud. |
| Target off-center | Target at X=3 instead of lane center X=0. Shifted all target parts to X=0. |
| Mountain blocking view | Mountain 7 at Z=-0.7 instead of backdrop zone Z=95-170. Moved to Z=130. |
| TargetArchway missing | Rebuilt with wood posts, cross beams, "Archery Legends / Greenwood Range" sign. |

**New Features:**
| Feature | Details |
|---------|---------|
| Accuracy spread system | Server-side spread in GameManager. BaseSpread=0.04 rad, reduced by power (60%) and SteadyHand shop item (50%). |
| Client arrow flight | BowController launches visible arrow along physics arc (gravity, direction, power). Auto-destroys on ground/past-target. |
| Arrow trail integration | Flying arrow shows ParticleEmitter matching equipped trail color from shop. |
| Lane extension | Target moved from Z=21 to Z=45 (50 stud range). Stone path, borders, torches extended. |
| Bow release sound | Replaced sword-clash sound (9114444008) with bow twang (6472453973 at 1.3x speed). |

**Sound Asset Refinement (research agent + manual fixes):**
| Sound | Old Asset | New Asset | Reason |
|-------|-----------|-----------|--------|
| Miss | 7112275565 (cash register!) | 624706518 | Was playing purchase sound on miss |
| HitBullseye | 6150774030 (2.8s) | 7128958209 | Sharper bell ding, 75+ favorites |
| HitInner | 1053296915 (Minecraft) | 3626698892 | Dedicated thud sound |
| HitOuter | 1053296915 (=Inner) | 3626698892 | Same thud, differentiated by 0.85x pitch |
| PurchaseSuccess | 5964495032 | 7112275565 | Proper cash register kaching |
| StreakChime | 1620077983 | 131573697 | Classic subtle bell |
| BowDraw | 9089204439 (1.8s) | kept | Fixed stop-on-release (was playing 6.6s) |
| BowRelease | 9114444008 (sword) | 6472453973 | Proper twang at 1.3x |

**Config Changes:**
- Added `Config.Physics.BaseSpread`, `PowerAccuracyScale`, `SteadyHandReduction`
- Updated `Config.Sounds` with all corrected asset IDs

**Playtest:** Zero script errors across all 12 scripts.

---

### 2026-03-27: Sound Integration (COMPLETE)

**Status:** COMPLETE

Created SoundManager module and wired all 16 audio instances into gameplay.

**SoundManager Module (ReplicatedStorage.Modules.SoundManager):**
- Clone-and-play pattern for overlapping sounds
- `play(name)` — play any sound by instance name
- `playZone(zone)` — maps hit zone names to hit sounds

**Volume/PlaybackSpeed Tuning:**
| Sound | Volume | Speed | Design |
|-------|--------|-------|--------|
| HitBullseye | 0.8 | 1.2 | Sharp, exciting, high pitch |
| HitInner | 0.7 | 1.0 | Solid baseline |
| HitOuter | 0.6 | 0.85 | Lower pitch, duller |
| HitEdge | 0.5 | 0.7 | Dullest, least rewarding |
| Miss | 0.4 | 1.0 | Subtle swoosh |
| BowDraw | 0.5 | 1.0 | Ambient tension |
| BowRelease | 0.7 | 1.1 | Snappy twang |
| LevelUp | 0.8 | 1.0 | Celebration |
| StreakChime | 0.5 | 1.0 | Subtle positive |
| StreakBreak | 0.4 | 0.8 | Low disappointment |
| ButtonClick | 0.3 | 1.2 | Quick UI tick |
| PurchaseSuccess | 0.6 | 1.0 | Reward confirmation |
| VoiceTaunt | 0.4 | 0.9 | Slightly deep |
| VoiceCheer | 0.5 | 1.15 | Bright, upbeat |
| VoiceGroan | 0.4 | 0.7 | Deep, disappointed |
| VoiceReady | 0.5 | 1.0 | Neutral alert |

**Wiring Points:**
| Script | Sound | Trigger |
|--------|-------|---------|
| BowController | BowDraw | Mouse down (draw start) |
| BowController | BowRelease | Mouse up (fire) |
| HUDController | HitBullseye/Inner/Outer/Edge/Miss | ArrowResult event (per zone) |
| HUDController | LevelUp | Level up in round end |
| ShopController | ButtonClick | Equip success |
| ShopController | PurchaseSuccess | Purchase success |
| DailyRewardController | PurchaseSuccess | Claim reward |

**Playtest:** Zero errors across all scripts.

---

### 2026-03-27: UI Polish Pass (COMPLETE)

**Status:** COMPLETE

Full UI polish pass across all 5 client controllers.

**Duel Button Restyle (green theme):**
| Change | Details |
|--------|---------|
| BackgroundColor3 | Blue (80,80,180) → HUD green (15,25,18) |
| UIStroke | Blue (120,120,220) → green border (50,100,60) |
| Font | GothamBold → GothamBlack (match HUD) |
| Size | 140x40 → 140x50 (touch target) |
| Position | (20,-110) → (12,-125) aligned with HUD bar |
| All reset states | Updated (hideDuelUI, leaveQueue, leftQueue) |

**Popup Consistency Fixes:**
| Fix | Script | Change |
|-----|--------|--------|
| Shop action button height | ShopController | 28px → 36px |
| Duel result button | DuelController | 120x40 → 140x44 |
| DailyReward panel color | DailyRewardController | (25,25,35) → (30,30,45) |
| DailyReward title font | DailyRewardController | GothamMedium → GothamBold |
| Leaderboard close button | LeaderboardController | 30x30 → 32x32 |
| Leaderboard title size | LeaderboardController | 22 → 24 |

**Mobile Responsive Panels:**
| Panel | Old Size | New Size | MaxSize |
|-------|----------|----------|---------|
| Shop | 520x480 fixed | 92%W × 85%H | 520x480 |
| DailyReward | 460x380 fixed | 92%W × 70%H | 460x380 |
| Duel HUD | 400x100 fixed | 85%W × 100px | 400x100 |
| Duel Turn Indicator | 250x40 fixed | 60%W × 40px | — |
| Duel Result | 350x250 fixed | 85%W × 260px | 350x260 |
| Round End | 30%W × 50%H | 80%W × 60%H | 350x380 |

**Animation updates:** DailyReward show/hide tweens updated from fixed offsets to scale-based.

**Playtest:** Zero script errors. Only expected DataStore warnings (Studio API access disabled).

---

### 2026-03-27: Environment Overhaul + World Bow + Sounds (COMPLETE)

**Status:** COMPLETE

Major session covering world bow, full environment rebuild to match concept art, HUD polish, and sound assets.

**World Bow (replaced ViewportFrame approach):**
| Feature | Implementation |
|---------|----------------|
| Approach pivot | Switched from ViewportFrame overlay to world-space welded bow |
| Bow model | 12 parts: grip, grip wrap, upper/lower limbs, nock tips, string (2 segments), arrow (shaft, head, 2 fletches) |
| Attachment | WeldConstraint to character LeftHand (R15) or Left Arm (R6) |
| Draw animation | String segments + arrow track grip position, pull back proportional to currentPower |
| Fire animation | Arrow hides on fire, re-nocks after 0.4s delay |
| Skin support | applySkin() recolors limbs from Config.ShopItems.BowSkins Color |
| Lifecycle | Creates on CharacterAdded, destroys on death |

**Environment Rebuild (matching concept art):**
| Element | Details |
|---------|---------|
| Lighting | ClockTime 10.5, Atmosphere (misty), ColorCorrection (warm), Bloom |
| Ground | LeafyGrass material, lush green |
| Forest | 54 trees: mixed pine (conical, 3-layer) + deciduous (round canopy), pushed to X=18-58 |
| Mountains | 8 peaks with ridges + snow caps, Z=95-170, FileMesh cones |
| Shooting Deck | Open 4-post pavilion, angled wood plank roof, side/back rails, front step |
| Stone Path | 5-stud wide Slate strip with Cobblestone borders, Z=-1 to Z=27 |
| Target Archway | 14-stud wide, 21.75-stud tall posts, cross beams, sign board |
| Sign | "Archery Legends" (gold Fantasy font) + divider + "Greenwood Range" (green), text strokes for legibility |
| Torches | 10 lane torches at X=+-5, Fire + PointLight, every 6 studs |
| Lake | Preserved from previous build |

**Cleanup performed:**
- Removed old firing_platform, decorations, spectator_area, ground_details, ShootingLane, EnvironmentDetail, arena_monuments, arena_banners, LaneFencing, Campfire, old GateArchways
- Removed target easel per user request

**HUD Changes:**
| Change | Details |
|--------|---------|
| Layout reorder | Score moved to top, Daily Streak moved to bottom |
| Streak hidden when 0 | streakLabel + streakValue set Visible=false when streak is 0 |
| Fixed xpBarFrame bug | Practice mode referenced undefined xpBarFrame, fixed to xpBarBg |

**Sound Assets (16 instances in ReplicatedStorage.Audio):**
| Sound | Asset ID | Status |
|-------|----------|--------|
| BowDraw | 9113081793 | Working |
| BowRelease | 9114444008 | Working |
| HitBullseye | 6472453973 | Working |
| HitInner | 1053296915 | Working |
| HitOuter | 1053296915 | Working |
| HitEdge | 6472453973 | Working |
| Miss | 2235655773 | Working |
| LevelUp | 2686079706 | Working |
| StreakChime | 5826672935 | Working |
| StreakBreak | 2235655773 | Working |
| ButtonClick | 6895079853 | Working |
| PurchaseSuccess | 2686079706 | Working |
| VoiceTaunt | 2235655773 | Working |
| VoiceCheer | 5826672935 | Working |
| VoiceGroan | 2235655773 | Working |
| VoiceReady | 6895079853 | Working |

**Config.Sounds also updated to match.**

**Playtest:** Zero sound errors, zero script errors. Only expected DataStore warnings (Studio API access disabled).

---

### 2026-03-27: First-Person Bow Design Session (SUPERSEDED)

**Status:** SUPERSEDED by world bow approach above

Original design was ViewportFrame overlay. Pivoted to world-space welded bow for better visual integration.

---

### 2026-03-26: Phase 6 Complete — Duel Mode, Game Passes, Code Quality (COMPLETE)

**Status:** COMPLETE

Completed final Phase 6 features: Duel Mode, Game Passes, and Code Quality Audit.

**Arena Fixes:**
| Issue | Fix |
|-------|-----|
| Spawn at Y=0 (underground) | Moved to (0, 3, -5) |
| Spawn facing away from target | Changed orientation to (0, 0, 0) |
| Banner not visible | Created "ARCHERY LEGENDS" banner at Y=18, Z=35 above target |
| Limited ambiance | Added AmbientParticles with DustMotes and Pollen |

**DuelManager.server.luau** (ServerScriptService):
| Feature | Implementation |
|---------|----------------|
| Matchmaking queue | Players join/leave queue, auto-match when 2 available |
| Duel state machine | active -> finished/abandoned states |
| Turn management | Alternating turns, 5 arrows each player |
| Score tracking | Per-player score, bullseyes, arrow history |
| Winner determination | Highest score wins; bullseyes break ties |
| Rewards | 2x XP/currency winner, 0.5x loser (with Game Pass multipliers) |

**GamePassManager.server.luau** (ServerScriptService):
| Feature | Implementation |
|---------|----------------|
| VIP Pass (299R) | 2x XP multiplier, [VIP] chat tag |
| Double Currency (149R) | 2x currency multiplier |
| Radio Pass (99R) | CanPlayAudio flag (future feature) |

**Code Quality Audit:** Rate limiting, input validation, state guards on all remotes.

**Playtest:** Zero errors, all scripts initialize correctly.

---

### 2026-03-26: Phases 3-5 (COMPLETE)

- Phase 3: DataStore persistence, XP/currency awards
- Phase 4: XP bar, daily rewards, leaderboards
- Phase 5: Daily Reward UI, Leaderboard UI, Shop system
- Phase 6: Practice Mode (unlimited arrows, no persistence)

---

### 2026-03-25: Phases 1-2 + Foundation (COMPLETE)

- Operational structure (_ops/, .claude/)
- Phase 1: Arena, target, Config, Types, Remotes
- Arena visual polish (terrain, particles, torches)
- Phase 2: BowController, arrow flight, hit detection, round lifecycle, HUD

---

## Document History

| Date | Change |
|------|--------|
| 2026-03-25 | Initial PROGRESS.md, Phases 1-2, arena polish |
| 2026-03-26 | Phases 3-6 complete, MVP finished |
| 2026-03-27 | World bow, environment overhaul, HUD reorder, sound assets |
