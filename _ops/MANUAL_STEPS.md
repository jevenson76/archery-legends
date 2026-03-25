# Manual Steps Required

**Project:** Archery Legends
**Purpose:** Track tasks that require manual action in Roblox Studio (cannot be automated via MCP)

---

## Pending Manual Steps

### 1. Add Ambient Audio (Priority: Low)

**Reason:** Roblox Audio Privacy Update (March 2022) restricts programmatic audio asset loading. Sounds must be added via Studio's Audio Library.

**Steps:**
1. Open Roblox Studio
2. Go to **View → Asset Manager**
3. Click **Audio Library** tab
4. Search and add the following sounds:

| Sound Type | Suggested Search | Parent Location | Settings |
|------------|------------------|-----------------|----------|
| Birds/Nature | "forest birds ambient" | Create `workspace.AmbientSounds` folder | Volume: 0.2, Looped: true |
| Wind | "gentle wind ambient" | `workspace.AmbientSounds` | Volume: 0.15, Looped: true |
| Fire Crackling | "fire crackling loop" | Each `workspace.Torches.Torch_N.FirePoint` | Volume: 0.12, Looped: true, RollOff: 5-25 studs |
| Water Stream | "water stream ambient" | Near pond at (-32, 0, -27) | Volume: 0.2, Looped: true, RollOff: 10-40 studs |

**Status:** PENDING

---

## Completed Manual Steps

(None yet)

---

## Notes

- MCP tools can create Sound instances but cannot load audio assets due to Roblox permissions
- All visual effects (particles, lights, terrain) work via MCP
- Game Passes and Developer Products must be configured in Roblox Creator Dashboard

---

## Document History

| Date | Change |
|------|--------|
| 2026-03-25 | Initial MANUAL_STEPS.md created |
