# Archery Legends: AAA Visual Overhaul Design

**Date:** 2026-03-26
**Status:** Approved
**Inspiration:** Gemini-generated concept art showing medieval forest archery range

## Overview

Comprehensive 10-part visual and UX overhaul to bring Archery Legends from MVP quality to AAA Roblox game feel. All changes executed via MCP Luau scripts and client script rewrites.

## Part 1: Ground Overhaul
- Replace arena_ground material from current to Grass (green)
- Ground color: RGB(60, 120, 50) - lush forest green
- Keep cobblestone lane as contrast path
- Add dirt patches only around high-traffic areas (platform, target base)

## Part 2: Banner - Wooden Gate/Archway
- Delete existing GameBanner model
- Build thick wooden A-frame gate behind target
- "ARCHERY LEGENDS" as mounted sign on crossbeam (SurfaceGui, Front face)
- "Greenwood Range" plaque below
- Torch holders on each post with fire particles
- Posts: thick (2x2), dark wood material

## Part 3: HUD - Full Info Panel
- Single unified dark-green panel (upper-right)
- Contents (top to bottom): Daily Streak + fire icon, Score, Level + XP bar, Arrows Left, Arrow Type
- All GothamBlack font, white text, green accents
- Scale-based sizing for mobile

## Part 4: Range Data Panel
- Bottom-right floating panel
- Distance to target, Wind Speed, Wind Direction
- Small icons next to each line
- Dark-green background matching HUD

## Part 5: Buttons - Icon + Text
- Two buttons: STORE (bag icon + text), LEADERBOARD (trophy icon + text)
- Wider buttons (~80x52) to fit icon above text
- Gold icons, white text labels
- Dark green backgrounds

## Part 6: First-Person Bow
- ViewportFrame or Model attached to Camera
- Visible in lower-center of screen during gameplay
- Shows equipped bow skin
- Fire/ice effects on nocked arrow when trail equipped

## Part 7: Forest Density
- 50+ additional trees at varied heights (3-10 studs)
- Dense on perimeter, thinning toward lane
- 4 green shades for variety
- Undergrowth: small bush spheres near ground level

## Part 8: Water Feature - Lake
- Remove small scattered ponds
- One large lake (20x15 studs) to the right of the lane
- Glass material, blue tint, 0.3 transparency
- Stone rim, lily pads, wooden dock/pier

## Part 9: Lane Fencing
- Remove existing arena_fencing
- Split-rail wooden fence both sides of lane
- Posts every 5 studs, two horizontal rails
- Platform to target area (~30 studs)

## Part 10: Atmosphere
- Lighting: ClockTime 15 (golden hour), warmer ambient
- Atmosphere: density 0.3, green-tinted haze
- Campfire near platform with fire+smoke particles
- Enhanced torch effects
- Color correction: slightly deeper greens
- Bloom and sun rays tuned for forest mood
