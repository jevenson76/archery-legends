# Audio System Design — Archery Legends

**Date:** 2026-03-26
**Status:** Approved
**Author:** Claude + Jason

---

## Overview

Implement a stylized/punchy audio system with 16 sounds covering bow mechanics, hit feedback, UI events, and character voices. Client-only architecture for zero-latency feedback.

## Requirements

- **Style:** Stylized/punchy arcade feel (not realistic)
- **Scope:** Core mechanics + UI + character voices
- **Source:** Open-source sounds (CC0/CC-BY)
- **Architecture:** Client-only via SoundService (Approach A)

## Sound List (16 Total)

### Core Sounds (7)

| ID | Trigger | Description |
|----|---------|-------------|
| `BowDraw` | Hold mouse to draw | Rising tension, string creak |
| `BowRelease` | Release arrow | Sharp twang, satisfying snap |
| `HitBullseye` | Bullseye zone hit | High-pitched "thwack" + subtle chime |
| `HitInner` | Inner ring hit | Clean impact, medium pitch |
| `HitOuter` | Outer ring hit | Softer thud |
| `HitEdge` | Edge zone hit | Dull thunk |
| `Miss` | Arrow misses target | Distant thud on backdrop |

### UI Sounds (5)

| ID | Trigger | Description |
|----|---------|-------------|
| `LevelUp` | Player levels up | Triumphant fanfare (short, 1-2 sec) |
| `StreakChime` | Streak counter increments | Ascending chime |
| `StreakBreak` | Streak resets on miss | Deflating "womp" |
| `ButtonClick` | UI button pressed | Crisp click |
| `PurchaseSuccess` | Shop purchase confirmed | Cash register "cha-ching" |

### Character Voice Sounds (4)

| ID | Trigger | Description |
|----|---------|-------------|
| `VoiceTaunt` | Player taunts in duel | Playful mocking gibberish (Simlish-style) |
| `VoiceCheer` | Win duel / bullseye streak | Excited celebration babble |
| `VoiceGroan` | Lose duel / miss badly | Disappointed "aww" mumble |
| `VoiceReady` | Round starts / duel matched | Confident "let's go" energy |

## Architecture

### File Structure

```
StarterPlayerScripts/
  AudioManager.client.luau    -- Central sound controller

ReplicatedStorage/
  Audio/                      -- Folder containing Sound instances
    BowDraw (Sound)
    BowRelease (Sound)
    HitBullseye (Sound)
    HitInner (Sound)
    HitOuter (Sound)
    HitEdge (Sound)
    Miss (Sound)
    LevelUp (Sound)
    StreakChime (Sound)
    StreakBreak (Sound)
    ButtonClick (Sound)
    PurchaseSuccess (Sound)
    VoiceTaunt (Sound)
    VoiceCheer (Sound)
    VoiceGroan (Sound)
    VoiceReady (Sound)
```

### AudioManager API

```lua
local AudioManager = {}

-- Play a sound once
AudioManager.Play(soundId: string, options: {volume: number?, pitch: number?}?)

-- Play a sound with random pitch variation (for variety)
AudioManager.PlayVaried(soundId: string, pitchRange: {min: number, max: number}?)

-- Loop a sound (returns stop function)
AudioManager.Loop(soundId: string): () -> ()

-- Stop a specific sound
AudioManager.Stop(soundId: string)

-- Stop all sounds
AudioManager.StopAll()

-- Preload all sounds (called on init)
AudioManager.Preload()
```

### Integration Points

| Controller | Sounds Used |
|------------|-------------|
| BowController | BowDraw (loop while drawing), BowRelease |
| HUDController | HitBullseye/Inner/Outer/Edge, Miss, LevelUp, StreakChime, StreakBreak |
| ShopController | ButtonClick, PurchaseSuccess |
| DuelController | VoiceTaunt, VoiceCheer, VoiceGroan, VoiceReady, ButtonClick |

## Sound Sourcing

### Sources (Open License)

| Library | URL | License | Best For |
|---------|-----|---------|----------|
| Freesound.org | freesound.org | CC0/CC-BY | Bow mechanics, impacts |
| Kenney.nl | kenney.nl/assets | CC0 | UI sounds, chimes |
| OpenGameArt.org | opengameart.org | CC0/CC-BY | Character voices |
| Mixkit.co | mixkit.co | Free | Punchy impacts |

### Sound Specifications

- **Format:** OGG or MP3 (Roblox compatible)
- **Sample rate:** 44.1kHz
- **Channels:** Mono preferred (smaller files)
- **Duration:** Under 2 seconds (except LevelUp: up to 3 sec)
- **File size:** Under 1MB each
- **Style:** Clean attack, short decay, punchy

## Implementation Flow

1. Search and download 16 sounds from open-source libraries
2. Create Audio folder in ReplicatedStorage with Sound instances
3. User uploads audio files to Roblox Creator Dashboard
4. Wire asset IDs into Config.Sounds
5. Create AudioManager.client.luau
6. Integrate into BowController, HUDController, ShopController, DuelController
7. Playtest and tune volumes/pitch
8. Add taunt button to DuelController UI

## Volume Mixing

| Category | Base Volume | Notes |
|----------|-------------|-------|
| Bow mechanics | 0.8 | Prominent, satisfying |
| Hit feedback | 1.0 | Most important — feel-good |
| UI clicks | 0.5 | Subtle, not annoying |
| Level up/Purchase | 0.7 | Celebratory but not jarring |
| Character voices | 0.6 | Fun but not overwhelming |

## Success Criteria

- [ ] All 16 sounds sourced and uploaded
- [ ] Zero latency on bow draw/release
- [ ] Hit sounds feel satisfying and distinct per zone
- [ ] Character voices add personality without being annoying
- [ ] No audio clipping or distortion
- [ ] Playtest confirms "AAA feel"
