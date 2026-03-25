# Engagement Psychology — Design Reference

## Core Loops

### Primary Loop (per-round, 2-5 minutes)
Aim → Shoot → Hit/Miss Feedback → Score → Reward → Repeat

- Immediate feedback: satisfying hit sounds, particle effects, score popups
- Variable ratio reinforcement: occasional critical hits, bonus targets, rare drops
- Near-miss psychology: arrows that barely miss show how close they were
- Escalating difficulty within a round keeps flow state

### Secondary Loop (per-session, 10-30 minutes)
Play rounds → Earn XP/currency → Level up → Unlock content → Play more

- Clear progression bar always visible on HUD
- "Almost there" indicators when close to next unlock
- End-of-session summary showing progress toward goals

### Tertiary Loop (daily/weekly)
Daily login → Claim rewards → Complete challenges → Earn exclusives

- Streak-based daily rewards (escalating value, reset on miss)
- Weekly challenges requiring multiple sessions
- Limited-time events creating urgency

## Psychological Tactics (Mapped to Implementation)

### 1. Onboarding (First 60 Seconds)
- Tutorial lets player hit bullseye within 30 seconds (instant competence feeling)
- Free cosmetic item gifted during tutorial (endowment effect — they now "own" something)
- Show other players' rare items in lobby (aspiration gap)
- First reward within 60 seconds of gameplay

### 2. Progression Systems
- **XP & Levels**: Level badge visible next to name. Prestige system after max.
- **Mastery Tracks**: Per-bow mastery, per-arena mastery (completionism)
- **Battle Pass**: Free + premium tiers. 30-day seasons. ~40 tiers each.
- **Achievement Badges**: Roblox native badges (10 games, 100 bullseyes, level milestones)
- **Skill Rankings**: Bronze → Silver → Gold → Diamond → Legend

### 3. Social Pressure & Competition
- Leaderboards: daily, weekly, all-time, friends-only
- 1v1 Duels: direct friend challenges
- Clans/Guilds: clan wars, shared progression, clan cosmetics
- Spectator mode: watch top players
- "Your friend passed you on the leaderboard" notification

### 4. Collection & Customization
- Bow rarity tiers: Common → Uncommon → Rare → Epic → Legendary
- Arrow trail effects: colors, particles, sound effects
- Arena themes: forest, castle, space, underwater (unlock progressively)
- Player titles earned through gameplay ("Sharpshooter", "Eagle Eye")

### 5. FOMO & Urgency
- Limited-time seasonal bows (Halloween, Christmas, Summer)
- Weekend tournaments with exclusive rewards
- Rotating shop with countdown timers
- Event-exclusive arenas that disappear after the event

### 6. Variable Reward Schedules
- Random rare drops after matches (variable ratio reinforcement)
- Mystery chests earned through gameplay milestones (never purchased)
- "Lucky shot" bonus that randomly appears on targets
- Critical hit system with flashy effects on high-accuracy shots

### 7. Loss Aversion & Sunk Cost
- Daily streak counter with visible day count
- Season pass progress bar (already invested time)
- Gentle ranking decay if inactive (lose rank slowly, never lose items)
- "Continue your streak!" reminder on login

### 8. Session Architecture
- Quick Match: 2-3 minutes (low barrier to start)
- Tournament: 5-10 minutes (deeper commitment)
- Practice Range: unlimited, no pressure (zen mode)
- Post-match: XP gained, challenges progressed, "Next reward in X points", "Play Again" button
- No natural stopping points — always one more thing to chase

### 9. Roblox Algorithm Signals
Design for the metrics Roblox rewards in discovery:
- Maximize: play time, return visits, social invites, thumbs up ratio
- Prompt thumbs-up after a great round (contextual, not random)
- "Invite friend" with bonus reward for both players
- Premium Payouts: design for premium player session time
