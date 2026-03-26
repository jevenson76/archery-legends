# Archery Legends — Game Design Document

## 1. Game Overview

### Elevator Pitch
A fast-paced, skill-based archery game where players master the bow, climb competitive rankings, and collect rare cosmetics. Think "Flappy Bird meets eSports" — simple to pick up, impossible to master.

### Genre
Casual Competitive / Sports Simulation

### Unique Selling Proposition (USP)
- **Feel-good physics:** Satisfying arrow flight with perfect "thwack" feedback
- **Skill-based progression:** Difficulty tiers let beginners succeed while veterans chase mastery
- **Cosmetic depth:** 50+ bows, trails, and titles to collect without any pay-to-win

### Target Audience
- **Primary:** Roblox players ages 9-16 seeking competitive casual games
- **Secondary:** Achievement hunters / collectors who completionist grind
- **Tertiary:** Streamers looking for satisfying skill-shot content

### Success Metrics
| Metric | Target | Why |
|--------|--------|-----|
| D1 Retention | 40%+ | First-day hook matters most |
| D7 Retention | 20%+ | Weekly challenge loop working |
| Avg Session Time | 12+ minutes | 3-4 rounds per session |
| % Monetized Players | 5%+ | Cosmetic appeal landing |

---

## 2. Core Mechanic — Archery Physics

### Input Flow
1. **Aim:** Mouse position controls bow angle
2. **Draw:** Hold left click to build power (0-100% over 1.5 seconds)
3. **Release:** Let go to fire

### Physics Model (Difficulty-Based)

| Difficulty | Gravity | Wind | Target Distance | XP Multiplier |
|------------|---------|------|-----------------|---------------|
| **Casual** | None | None | 20 studs | 1.0x |
| **Normal** | Yes | None | 30 studs | 1.5x |
| **Expert** | Yes | Yes | 40 studs | 2.0x |

**Gravity formula (Normal/Expert):**
```
dropDistance = 0.5 * gravity * (flightTime ^ 2)
gravity = 196.2 (Roblox default)
flightTime = distance / (arrowSpeed * powerPercent)
```

**Wind formula (Expert only):**
```
windDrift = windStrength * flightTime * windDirection
windStrength = random(0.5, 2.0) per round
windDirection = Vector3 with random X/Z components
```

### Scoring Zones

| Zone | Radius (studs) | Points | Visual |
|------|----------------|--------|--------|
| **Bullseye** | 0.5 | 10 | Gold center, particle burst |
| **Inner Ring** | 1.5 | 7 | Red ring |
| **Outer Ring** | 3.0 | 4 | Blue ring |
| **Edge** | 4.5 | 1 | White ring |
| **Miss** | >4.5 | 0 | Arrow sticks to backdrop |

### Feel & Feedback

**On Hit:**
- Particle burst at impact point (color matches zone)
- Score popup rises from target (BillboardGui)
- Satisfying "thwack" sound (pitch varies by zone — higher = better)
- Camera micro-shake on bullseye
- Streak counter increments with bonus chime

**On Miss:**
- Arrow sticks to backdrop with dull thud
- "Near miss" indicator shows distance to nearest zone
- Streak resets with subtle deflation sound

**On Draw:**
- Bow string tension visual (string pulls back)
- Power meter fills with subtle vibration
- Aim arc shows predicted trajectory (fades at low power)

---

## 3. Game Modes

### Quick Match (MVP)
- **Player count:** 1 (solo against personal best)
- **Duration:** 10 arrows, ~2-3 minutes
- **Rules:** Shoot 10 arrows, maximize score
- **Scoring:** Sum of all arrow scores + accuracy bonus
- **End condition:** All 10 arrows fired
- **Rewards:** XP, currency, chance at random drop

### 1v1 Duel (MVP)
- **Player count:** 2
- **Duration:** 10 arrows total (5 each), ~3-4 minutes
- **Rules:** Alternating turns. Player A shoots, then Player B. Repeat 5x.
- **Scoring:** Highest total score wins. Ties go to player with more bullseyes.
- **End condition:** Both players fire 5 arrows
- **Rewards:** Winner gets 2x XP/currency, loser gets 0.5x. Ranking points adjust.
- **Matchmaking:** Simple queue. Match players within 2 skill ranks.

### Practice Range (MVP)
- **Player count:** 1
- **Duration:** Unlimited
- **Rules:** No scoring, no rewards. Pure practice.
- **Features:** Target distance slider (10-50 studs), difficulty toggle, trajectory guide always visible
- **Purpose:** Skill building without pressure

### Tournament (Post-Launch)
- **Player count:** 8-16 bracket
- **Duration:** ~20-30 minutes full bracket
- **Rules:** Single elimination 1v1s
- **Rewards:** Exclusive tournament titles, currency jackpot
- **Frequency:** Every 2 hours, announced 10 minutes prior

---

## 4. Progression Systems

### XP & Leveling

**XP Sources:**
| Source | Base XP | Notes |
|--------|---------|-------|
| Round completion | 50 | Always earned |
| Score bonus | score / 2 | Higher scores = more XP |
| Accuracy bonus | bullseyes * 10 | Rewards precision |
| Difficulty multiplier | 1x / 1.5x / 2x | Casual / Normal / Expert |
| Win bonus (Duels) | +100 | Duels only |

**Level Curve:**
```
XP_required(level) = floor(100 * level ^ 1.5)
```

| Level | XP Required | Cumulative |
|-------|-------------|------------|
| 1→2 | 100 | 100 |
| 5→6 | 559 | 1,854 |
| 10→11 | 1,000 | 5,873 |
| 25→26 | 3,125 | 32,183 |
| 50→51 | 8,839 | 115,789 |
| 100 | MAX | ~400,000 |

**Max Level:** 100
**Prestige:** At level 100, can reset to level 1 with a prestige badge (up to 10 prestiges)

### Skill Rankings

| Rank | Points Required | % of Players |
|------|-----------------|--------------|
| Bronze | 0-999 | 40% |
| Silver | 1000-2499 | 30% |
| Gold | 2500-4999 | 20% |
| Diamond | 5000-9999 | 8% |
| Legend | 10000+ | 2% |

**Rank Point Changes (Duels):**
- Win: +25 points (+10 bonus vs higher rank)
- Loss: -15 points (-5 penalty vs lower rank)
- Daily decay: -10 points if no games played (minimum: rank floor)

### Mastery Tracks (Post-Launch)

**Bow Mastery:** Use a specific bow for 100 kills to unlock its "Mastered" variant (visual upgrade)
**Arena Mastery:** Complete 50 rounds in an arena to unlock arena-specific title

### Battle Pass Structure

- **Season Length:** 30 days
- **Total Tiers:** 40
- **XP per Tier:** 1000 (scales slightly at higher tiers)
- **Free Track:** Every tier (currency, basic items, XP boosts)
- **Premium Track:** Alternate tiers (exclusive skins, trails, titles)
- **Premium Price:** 399 Robux

**Tier Reward Distribution:**
| Tier Range | Free Reward | Premium Reward |
|------------|-------------|----------------|
| 1-10 | Currency (50-150) | Common trails, XP boosts |
| 11-20 | Currency (150-300), 1 uncommon | Uncommon bows, titles |
| 21-30 | Currency (300-500), 2 uncommon | Rare bows, premium trails |
| 31-39 | Currency (500+), rare item | Epic items, exclusive emotes |
| 40 | Legendary item | Season-exclusive legendary bow |

---

## 5. Monetization

### Game Passes (One-Time Purchase)

| Pass | Price | Benefits | Psychology |
|------|-------|----------|------------|
| **VIP Pass** | 299 R | 2x XP, [VIP] chat tag, VIP practice range | Status symbol, progression accelerator |
| **Double Currency** | 149 R | 2x currency earnings | Collection accelerator |
| **Radio Pass** | 99 R | Play audio in lobby | Social expression |

### Developer Products (Repeatable)

**Arrow Trails:**
| Item | Price | Rarity | Visual |
|------|-------|--------|--------|
| Fire Trail | 49 R | Common | Orange flame particles |
| Ice Trail | 49 R | Common | Blue frost particles |
| Lightning Trail | 75 R | Uncommon | Electric sparks |
| Rainbow Trail | 99 R | Uncommon | Color cycling |
| Galaxy Trail | 149 R | Rare | Starfield particles |
| Void Trail | 199 R | Epic | Black hole effect |

**Bow Skins:**
| Item | Price | Rarity | Visual |
|------|-------|--------|--------|
| Shadow Bow | 149 R | Uncommon | Dark material, smoke effect |
| Gold Bow | 299 R | Rare | Metallic gold, shine effect |
| Crystal Bow | 499 R | Epic | Translucent with inner glow |
| Dragon Bow | 799 R | Legendary | Dragon head limbs, fire accent |

**Currency Packs:**
| Pack | Price | Amount | Bonus |
|------|-------|--------|-------|
| Starter | 75 R | 500 | — |
| Value | 199 R | 1500 | +10% |
| Premium | 399 R | 3500 | +20% |

### Psychological Rationale

- **VIP at 299R:** Just below the psychological "300" barrier. Feels like a deal.
- **Bow skins 149-799R:** Clear rarity ladder. Players buy the 149 first, then aspire to 799.
- **Currency packs exist but aren't pushed:** Players can grind or buy. No pressure, but option exists.
- **No gameplay advantages:** All combat stats are equal. Cosmetic-only preserves fairness and avoids P2W backlash.

---

## 6. Engagement Systems

### Daily Rewards

| Day | Reward | Value |
|-----|--------|-------|
| 1 | 50 Currency | ~$0.02 equivalent |
| 2 | 100 Currency | |
| 3 | Random Common Trail | Hooks collectors |
| 4 | 200 Currency | |
| 5 | Random Uncommon Item | Excitement spike |
| 6 | 500 Currency | |
| 7 | Mystery Chest (Random Rare) | Weekly payoff |

**Streak Rules:**
- Claim within 24 hours to continue streak
- Missing a day resets streak to Day 1
- After Day 7, cycle repeats with +25% currency bonus (stacks up to 4x)

**UI:** Calendar grid showing claimed days with glow. Today's reward highlighted. "Claim" button pulses.

### Weekly Challenges (3 Active)

| Challenge Type | Example | Reward |
|----------------|---------|--------|
| Score-based | "Hit 25 bullseyes this week" | 300 Currency + 500 XP |
| Volume-based | "Play 15 rounds" | 200 Currency + 300 XP |
| Mode-specific | "Win 5 duels" | 500 Currency + 1000 XP |
| Difficulty-based | "Complete 3 Expert rounds" | Rare item + 750 XP |

**Refresh:** Every Monday at 00:00 UTC
**UI:** Progress bars on HUD, expandable panel with details

### FOMO Events Calendar

| Event | Duration | Content | Frequency |
|-------|----------|---------|-----------|
| Weekend Warrior | Fri-Sun | 2x XP | Weekly |
| Lucky Bullseye | Random 2hr | 3x chance for rare drops | 2-3x weekly |
| Tournament Weekend | Sat-Sun | Bracket tournaments every 2hr | Monthly |
| Seasonal Event | 2 weeks | Limited bows, themed arena | Quarterly |
| Anniversary | 1 week | All-time best rewards, legacy items | Yearly |

### Social Features

- **Friends Leaderboard:** See where you rank among friends
- **Invite Bonus:** Both players get 200 currency when invited friend plays first game
- **Spectate:** Watch live duels from lobby
- **"Passed You" Notification:** Alert when friend beats your high score

---

## 7. Content Inventory

### Launch Content (MVP+)

**Bows (5):**
| Name | Rarity | Source |
|------|--------|--------|
| Default Bow | Common | Starting item |
| Shadow Bow | Uncommon | Shop (149R) |
| Gold Bow | Rare | Shop (299R) |
| Crystal Bow | Epic | Shop (499R) |
| Battle Pass Bow | Legendary | Season 1 Tier 40 |

**Arrow Trails (6):**
| Name | Rarity | Source |
|------|--------|--------|
| None | — | Default |
| Fire | Common | Shop (49R) |
| Ice | Common | Shop (49R) |
| Lightning | Uncommon | Shop (75R) |
| Rainbow | Uncommon | Shop (99R) |
| Season Exclusive | Rare | Battle Pass |

**Arenas (2):**
| Name | Theme | Unlock |
|------|-------|--------|
| Training Grounds | Medieval courtyard | Default |
| Forest Clearing | Nature, dappled light | Level 5 |

**Titles (8):**
| Title | Requirement |
|-------|-------------|
| Newcomer | Default |
| Sharpshooter | 100 bullseyes |
| Eagle Eye | 500 bullseyes |
| Duel Champion | Win 50 duels |
| Streak Master | 14-day login streak |
| Veteran | Level 50 |
| Legend | Legend rank |
| Prestige I-X | Each prestige level |

**Badges (6):**
| Badge | Requirement |
|-------|-------------|
| First Shot | Complete tutorial |
| Getting Started | Play 10 rounds |
| Dedicated | Play 100 rounds |
| Bullseye Collector | 100 bullseyes |
| Rising Star | Reach Level 10 |
| Top Tier | Reach Level 50 |

### Post-Launch Content (Months 2-6)

**Bows:** Dragon Bow, Cyber Bow, Nature Bow, Seasonal variants (Halloween, Winter, Summer)
**Trails:** Galaxy, Void, Hearts, Snowflakes, Fireworks
**Arenas:** Castle Battlements, Space Station, Underwater Temple, Halloween Graveyard
**Modes:** Tournament, Team Duels (2v2), Target Rush (speed mode)
**Features:** Clans, Clan Wars, Mastery Tracks, Emotes

---

## 8. Technical Architecture

### Folder Structure (Roblox Studio)

```
game
├── ServerScriptService/
│   ├── GameManager.server.luau       -- Round lifecycle, scoring, hit detection
│   ├── DuelManager.server.luau       -- 1v1 matchmaking, turn sync
│   ├── DataManager.server.luau       -- DataStore CRUD, auto-save
│   ├── ShopManager.server.luau       -- ProcessReceipt, purchase validation
│   ├── LeaderboardManager.server.luau-- OrderedDataStore rankings
│   ├── ChallengeManager.server.luau  -- Weekly challenge tracking
│   └── DailyRewardManager.server.luau-- Streak logic, reward grants
│
├── ReplicatedStorage/
│   ├── Modules/
│   │   ├── Config.luau               -- All tuning constants
│   │   ├── ArrowPhysics.luau         -- Trajectory calculation (shared)
│   │   └── Types.luau                -- Type definitions
│   ├── Remotes/
│   │   ├── FireArrow                 -- RemoteEvent: client → server
│   │   ├── ArrowResult               -- RemoteEvent: server → client
│   │   ├── RoundEnd                  -- RemoteEvent: server → client
│   │   ├── DuelState                 -- RemoteEvent: server → client
│   │   ├── RequestDuel               -- RemoteEvent: client → server
│   │   ├── ChallengeProgress         -- RemoteEvent: server → client
│   │   ├── DailyRewardClaim          -- RemoteEvent: client → server
│   │   ├── DailyRewardResult         -- RemoteEvent: server → client
│   │   ├── PurchaseRequest           -- RemoteEvent: client → server
│   │   ├── GetLeaderboard            -- RemoteFunction: client ↔ server
│   │   └── GetPlayerData             -- RemoteFunction: client ↔ server
│   └── Assets/
│       ├── Bows/                     -- Bow models
│       ├── Arrows/                   -- Arrow models
│       └── Effects/                  -- Particle templates
│
├── StarterPlayerScripts/
│   ├── BowController.client.luau     -- Input handling, aim, fire
│   ├── CameraController.client.luau  -- Aim camera, spectate camera
│   └── UIController.client.luau      -- HUD updates, shop, popups
│
├── StarterGui/
│   ├── HUD/                          -- Score, XP bar, streak, challenge tracker
│   ├── ShopGui/                      -- Bow/trail store
│   ├── ProgressionGui/               -- Level, battle pass
│   ├── DailyRewardGui/               -- Calendar popup
│   ├── DuelGui/                      -- Matchmaking, turn indicator
│   └── ResultsGui/                   -- End-of-round summary
│
└── Workspace/
    ├── Arenas/
    │   ├── TrainingGrounds/
    │   └── ForestClearing/
    ├── Targets/
    └── SpawnLocations/
```

### RemoteEvent/RemoteFunction Definitions

| Name | Type | Direction | Payload |
|------|------|-----------|---------|
| FireArrow | Event | C→S | `{direction: Vector3, power: number, difficulty: string}` |
| ArrowResult | Event | S→C | `{hit: bool, zone: string, score: number, position: Vector3}` |
| RoundEnd | Event | S→C | `{totalScore: number, xpEarned: number, currencyEarned: number, newLevel: number?}` |
| DuelState | Event | S→C | `{phase: string, currentTurn: UserId, scores: {p1: number, p2: number}, arrowsLeft: {p1: number, p2: number}}` |
| RequestDuel | Event | C→S | `{mode: "queue" \| "invite", targetUserId?: number}` |
| ChallengeProgress | Event | S→C | `{challengeId: string, progress: number, target: number, completed: bool}` |
| DailyRewardClaim | Event | C→S | `{}` |
| DailyRewardResult | Event | S→C | `{success: bool, reward: {type: string, value: any}, newStreak: number}` |
| PurchaseRequest | Event | C→S | `{productId: number}` |
| GetLeaderboard | Function | C↔S | Request: `{type: "daily"\|"weekly"\|"alltime"\|"friends"}` → Response: `{{rank, userId, displayName, score}[]}` |
| GetPlayerData | Function | C↔S | Request: `{}` → Response: `PlayerData` |

### DataStore Schema

**Primary Store:** `PlayerDataStore`
**Key Format:** `Player_{UserId}`

```lua
type PlayerData = {
    -- Progression
    Level: number,           -- 1-100
    XP: number,              -- Current XP toward next level
    Prestige: number,        -- 0-10
    Currency: number,        -- Earned through gameplay

    -- Stats
    TotalGamesPlayed: number,
    TotalBullseyes: number,
    TotalScore: number,
    HighScore: number,
    DuelsWon: number,
    DuelsLost: number,

    -- Ranking
    SkillRank: string,       -- "Bronze", "Silver", etc.
    RankPoints: number,

    -- Daily/Weekly
    DailyStreak: number,
    LastLoginDate: string,   -- "YYYY-MM-DD"
    WeeklyChallenges: {
        [challengeId: string]: {
            progress: number,
            completed: boolean
        }
    },

    -- Inventory
    Inventory: {
        Bows: {string},      -- Array of owned bow IDs
        Trails: {string},    -- Array of owned trail IDs
        Titles: {string}     -- Array of owned title IDs
    },

    -- Equipped
    EquippedBow: string,
    EquippedTrail: string,
    EquippedTitle: string,
    EquippedDifficulty: string,  -- "Casual", "Normal", "Expert"

    -- Battle Pass
    SeasonId: string,        -- Current season identifier
    SeasonTier: number,      -- 0-40
    SeasonPremium: boolean,  -- Owns premium pass

    -- Receipts (for idempotent purchase processing)
    ProcessedReceipts: {string}  -- Array of processed receipt IDs
}
```

**Leaderboard Stores (OrderedDataStore):**
- `DailyHighScores_{YYYY-MM-DD}`
- `WeeklyHighScores_{YYYY-WW}`
- `AllTimeHighScores`

---

## 9. Roblox Algorithm Strategy

### Discovery Signal Optimization

| Signal | Design Decision |
|--------|-----------------|
| **Play Time** | No natural stopping points. Always one more challenge, one more level tick. End-of-round shows "Next reward in X points." |
| **Return Visits** | Daily rewards with streak. Weekly challenges. Limited-time events announced 24hr ahead. |
| **Social Invites** | "Invite friend" grants both players 200 currency. Prominent "Invite" button in lobby. |
| **Thumbs Up** | Prompt rating after a round where player hit 3+ bullseyes (positive emotional state). |
| **Premium Playtime** | Premium payouts incentivize designing for premium player session time. Premium-friendly pricing on passes. |

### First-Time User Experience (FTUE)

| Timing | Event |
|--------|-------|
| 0-30 seconds | Tutorial: guided aim, guaranteed bullseye ("Nice shot!") |
| 30-60 seconds | Free common trail gifted ("You earned a reward!") |
| 60-90 seconds | First full round on Casual |
| Post-round | Level up animation, XP bar progression, daily reward prompt |
| 2 minutes | "Play Again" with preview of next unlock |

### Session Pacing

```
[Join] → [Daily Reward Popup] → [Quick Match x2] → [Level Up!]
→ [Challenge Progress] → [Quick Match] → [Almost at next tier...]
→ [One more round] → [Win!] → [Play Again?]
```

No session should feel "done." Always leave a carrot dangling.

---

## 10. MVP Scope

### What Ships First (2-4 Weeks)

**Core Mechanic:**
- [x] Aim, draw, release bow
- [x] Arrow physics (Casual + Normal difficulty)
- [x] Hit detection with 4 scoring zones
- [ ] Visual/audio feedback on hit/miss (partial - audio requires manual setup)

**Game Modes:**
- [x] Quick Match (10 arrows, solo)
- [ ] 1v1 Duel (alternating turns, 5 arrows each)
- [ ] Practice Range (unlimited, no scoring)

**Progression:**
- [x] XP and leveling (to 100)
- [x] Currency earning
- [x] DataStore persistence

**Engagement:**
- [x] Daily rewards with streak
- [x] Daily/weekly/all-time leaderboards

**Content:**
- [x] 1 Arena (Training Grounds)
- [x] Default bow
- [ ] 2 difficulty levels (Casual, Normal) — only Normal implemented

**UI:**
- [x] HUD (score, XP bar, difficulty indicator)
- [x] Results screen
- [x] Daily reward popup
- [x] Leaderboard view

### Explicitly Deferred

- Expert difficulty (wind physics)
- Battle Pass system
- Shop and monetization
- Weekly challenges
- Badges
- Second arena
- All cosmetics beyond default
- Clans
- Tournaments
- Prestige system

### Definition of "MVP Done"

1. Player can join, see tutorial, hit target, earn score
2. Player can play Quick Match and 1v1 Duel
3. XP, level, currency, and stats persist across sessions
4. Daily rewards work with streak tracking
5. Leaderboards display top 50 for daily/weekly/all-time
6. Zero critical errors in playtest output
