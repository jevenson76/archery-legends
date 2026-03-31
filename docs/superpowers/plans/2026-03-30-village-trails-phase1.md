# Village + Trails Phase 1 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add themed trail extensions from hub perimeter to Greenwood and Castle ranges, blocking sightlines and creating an adventurous walking experience.

**Architecture:** Build sightline-blocking prop walls at hub edge, then extend themed paths with biome-appropriate props from hub to existing range entrances. Relocate Tavern and Outfitter to trails. Add range SpawnLocations with respawn logic.

**Tech Stack:** Roblox Studio via MCP (execute_luau, edit_script_lines, set_property), Luau scripting

---

## File Structure

| Component | Location | Responsibility |
|-----------|----------|----------------|
| Trail props | workspace (via execute_luau) | Physical world builds |
| SpawnLocations | workspace.SpawnLocations | Range respawn points |
| GameManager | game.ServerScriptService.GameManager | Respawn logic (set player.RespawnLocation on range entry) |
| HUDController | game.StarterPlayer.StarterPlayerScripts.HUDController | Zone detection boundaries may need adjustment |

---

### Task 1: Greenwood Sightline Blocker

**Build a 20-stud tall wall of dense foliage at the hub's north edge with a 6-stud gap for the trail entrance.**

- [ ] **Step 1: Determine exact position**

Hub center is (0, 1.5, -35). Hub radius is 75 studs. North rim = Z = -35 + 75 = Z = 40. But Greenwood deck is at Z = -5. So the blocker goes between hub rim and the deck area. Place at Z = 5 (just past hub edge, before the range starts).

```lua
-- execute_luau: Build Greenwood sightline blocker
local blockerFolder = Instance.new("Folder")
blockerFolder.Name = "GreenwoodTrail"
blockerFolder.Parent = workspace

-- Left tree wall (west of path)
local leftWall = Instance.new("Part")
leftWall.Name = "TreeWallLeft"
leftWall.Size = Vector3.new(30, 20, 4)
leftWall.Position = Vector3.new(-18, 11, 5)
leftWall.Anchored = true
leftWall.Material = Enum.Material.Grass
leftWall.BrickColor = BrickColor.new("Dark green")
leftWall.Parent = blockerFolder

-- Right tree wall (east of path)
local rightWall = Instance.new("Part")
rightWall.Name = "TreeWallRight"
rightWall.Size = Vector3.new(30, 20, 4)
rightWall.Position = Vector3.new(18, 11, 5)
rightWall.Anchored = true
rightWall.Material = Enum.Material.Grass
rightWall.BrickColor = BrickColor.new("Dark green")
rightWall.Parent = blockerFolder

-- Gap is 6 studs wide at X = -3 to X = 3
-- Add canopy arch over the gap
local archway = Instance.new("Part")
archway.Name = "TreeArch"
archway.Size = Vector3.new(8, 3, 4)
archway.Position = Vector3.new(0, 19, 5)
archway.Anchored = true
archway.Material = Enum.Material.Grass
archway.BrickColor = BrickColor.new("Forest green")
archway.Parent = blockerFolder
```

- [ ] **Step 2: Verify sightline is blocked**

```lua
-- execute_luau: Check if target at (0,7,45) is occluded from hub center (0,5,-35)
-- Visual check: set camera to hub center looking north
local camera = workspace.CurrentCamera
camera.CFrame = CFrame.lookAt(Vector3.new(0, 5, -35), Vector3.new(0, 7, 45))
print("Camera set to hub center looking at Greenwood target")
-- Player should see tree wall, NOT the target
```

---

### Task 2: Greenwood Trail Path + Props

**Build 80-stud dirt path from tree wall gap to shooting deck, with forest props.**

- [ ] **Step 1: Build dirt path segments (Z=5 to Z=-5, connecting to deck)**

The path actually needs to run from the sightline blocker at Z=5 backward to the shooting deck at Z=-5. But the Greenwood Range extends from Z=-5 (deck) to Z=45 (target). The hub is at Z=-35. So the trail runs from hub rim (~Z=-5 to Z=5 area) — wait, let me recalculate.

Hub center Z=-35, radius 75 = north rim at Z=40. But Greenwood deck is at Z=-5 with the path going to Z=45. The hub currently connects to Greenwood via existing paths. The sightline blocker needs to be between the hub and the range entrance.

Actually the trail runs THROUGH the existing gap between hub (Z=-35 center) and Greenwood deck (Z=-5). Distance = 30 studs. The sightline blocker goes at ~Z=-5 to Z=0 area.

```lua
-- execute_luau: Build Greenwood trail props
local trail = workspace:FindFirstChild("GreenwoodTrail")
if not trail then
    trail = Instance.new("Folder")
    trail.Name = "GreenwoodTrail"
    trail.Parent = workspace
end

-- Dirt path (transitions from cobblestone)
local dirtPath = Instance.new("Part")
dirtPath.Name = "DirtPath"
dirtPath.Size = Vector3.new(5, 0.15, 30)
dirtPath.Position = Vector3.new(0, 0.15, -5)
dirtPath.Anchored = true
dirtPath.Material = Enum.Material.Slate -- Closest to dirt
dirtPath.Color = Color3.fromRGB(120, 90, 50)
dirtPath.Parent = trail

-- 8 trees flanking path (4 per side)
for i = 0, 3 do
    for _, xSide in {-1, 1} do
        local z = -15 + i * 6
        local x = xSide * (5 + math.random(1, 4))

        -- Trunk
        local trunk = Instance.new("Part")
        trunk.Name = "TrailTree"
        trunk.Size = Vector3.new(1, 6 + math.random(0, 3), 1)
        trunk.Position = Vector3.new(x, trunk.Size.Y / 2, z)
        trunk.Anchored = true
        trunk.Material = Enum.Material.Wood
        trunk.BrickColor = BrickColor.new("Reddish brown")
        trunk.Parent = trail

        -- Canopy
        local canopy = Instance.new("Part")
        canopy.Shape = Enum.PartType.Ball
        canopy.Size = Vector3.new(6, 5, 6)
        canopy.Position = Vector3.new(x, trunk.Size.Y + 2.5, z)
        canopy.Anchored = true
        canopy.Material = Enum.Material.Grass
        canopy.BrickColor = BrickColor.new("Dark green")
        canopy.Parent = trail
    end
end

-- 6 fern clusters (3 parts each)
for i = 0, 5 do
    local z = -18 + i * 5
    local xSide = (i % 2 == 0) and -3.5 or 3.5
    for f = 1, 3 do
        local fern = Instance.new("Part")
        fern.Name = "Fern"
        fern.Size = Vector3.new(0.8, 1.2, 0.8)
        fern.Position = Vector3.new(xSide + (f-2)*0.5, 0.6, z + (f-2)*0.3)
        fern.Anchored = true
        fern.Material = Enum.Material.Grass
        fern.Color = Color3.fromRGB(40, 100 + math.random(0,30), 30)
        fern.CanCollide = false
        fern.Parent = trail
    end
end

-- 2 fallen logs
for i, z in {-12, -3} do
    local log = Instance.new("Part")
    log.Name = "FallenLog"
    log.Size = Vector3.new(4, 0.6, 0.6)
    log.Position = Vector3.new(0, 0.5, z)
    log.CFrame = CFrame.new(0, 0.5, z) * CFrame.Angles(0, math.rad(15 * i), 0)
    log.Anchored = true
    log.Material = Enum.Material.Wood
    log.BrickColor = BrickColor.new("Brown")
    log.Parent = trail
end

-- Stream crossing with bridge
local stream = Instance.new("Part")
stream.Name = "Stream"
stream.Size = Vector3.new(8, 0.1, 2)
stream.Position = Vector3.new(0, 0.05, -8)
stream.Anchored = true
stream.Material = Enum.Material.Glass
stream.Color = Color3.fromRGB(60, 140, 180)
stream.Transparency = 0.3
stream.Parent = trail

local bridge = Instance.new("Part")
bridge.Name = "Bridge"
bridge.Size = Vector3.new(5, 0.3, 2.5)
bridge.Position = Vector3.new(0, 0.3, -8)
bridge.Anchored = true
bridge.Material = Enum.Material.WoodPlanks
bridge.BrickColor = BrickColor.new("Brown")
bridge.Parent = trail

print("[Trail] Greenwood trail built: path, 8 trees, 18 ferns, 2 logs, stream + bridge")
```

- [ ] **Step 2: Verify part count**

```lua
-- execute_luau
local count = 0
local trail = workspace:FindFirstChild("GreenwoodTrail")
if trail then
    for _ in trail:GetDescendants() do count += 1 end
end
print("Greenwood trail parts:", count, "(budget: 60)")
```

---

### Task 3: Relocate Tavern to Greenwood Trail Midpoint

**Move "The Archer's Rest" from hub to the Greenwood trail midpoint (~Z=-10).**

- [ ] **Step 1: Move tavern model**

```lua
-- execute_luau: Relocate tavern
local hub = workspace.CommunityHub
local tavern = hub:FindFirstChild("ArchersRest")
if not tavern then warn("Tavern not found") return end

-- Calculate offset to move tavern to trail midpoint
-- Current tavern is at approximately (-35, Y, -65) in the hub
-- Target: X=8 (slightly off trail to the east), Z=-10
local targetPos = Vector3.new(8, 0, -10)

-- Get current position from first significant part
local floor = tavern:FindFirstChild("Floor")
if not floor then warn("Tavern floor not found") return end
local currentPos = Vector3.new(floor.Position.X, 0, floor.Position.Z)
local offset = targetPos - currentPos

-- Move all parts in tavern
for _, part in tavern:GetDescendants() do
    if part:IsA("BasePart") then
        part.Position = part.Position + offset
    end
end

-- Reparent to trail folder
local trail = workspace:FindFirstChild("GreenwoodTrail")
if trail then
    tavern.Parent = trail
end

print("[Trail] Tavern relocated to Greenwood trail midpoint")
```

- [ ] **Step 2: Verify tavern is accessible and visible from trail**

Visual check during playtest.

---

### Task 4: Castle Sightline Blocker

**Build a 20-stud tall stone wall at the hub's east edge with a narrow gate entrance.**

- [ ] **Step 1: Build stone wall blocker**

Castle Range is at X=85. Hub center X=0, radius 75 = east rim at X=75. But the castle corridor starts around X=62. Blocker goes at approximately X=55, between hub and corridor.

```lua
-- execute_luau: Build Castle sightline blocker
local castleTrail = Instance.new("Folder")
castleTrail.Name = "CastleTrail"
castleTrail.Parent = workspace

-- The castle gate is at ~60 degrees from hub center
-- Gate center approximately at (62, Y, 1)
-- We need the blocker between the hub and the gate
-- Place it at the hub rim area, roughly (45, Y, -10)

-- Left wall section
local leftWall = Instance.new("Part")
leftWall.Name = "StoneWallLeft"
leftWall.Size = Vector3.new(4, 20, 25)
leftWall.Position = Vector3.new(42, 11, -5)
leftWall.Anchored = true
leftWall.Material = Enum.Material.Cobblestone
leftWall.BrickColor = BrickColor.new("Dark stone grey")
leftWall.Parent = castleTrail

-- Right wall section
local rightWall = Instance.new("Part")
rightWall.Name = "StoneWallRight"
rightWall.Size = Vector3.new(4, 20, 25)
rightWall.Position = Vector3.new(42, 11, -30)
rightWall.Anchored = true
rightWall.Material = Enum.Material.Cobblestone
rightWall.BrickColor = BrickColor.new("Dark stone grey")
rightWall.Parent = castleTrail

-- Gate entrance (6-stud gap between walls at Z=-17)
-- Stone archway over the gap
local archway = Instance.new("Part")
archway.Name = "StoneArch"
archway.Size = Vector3.new(4, 3, 8)
archway.Position = Vector3.new(42, 19, -17)
archway.Anchored = true
archway.Material = Enum.Material.Cobblestone
archway.BrickColor = BrickColor.new("Medium stone grey")
archway.Parent = castleTrail

print("[Trail] Castle sightline blocker built")
```

- [ ] **Step 2: Verify sightline blocked from hub center**

---

### Task 5: Castle Trail Path + Props

**Build 90-stud flagstone path from stone wall gap to existing castle corridor with medieval props.**

- [ ] **Step 1: Build flagstone path and props**

```lua
-- execute_luau: Castle trail props
local trail = workspace:FindFirstChild("CastleTrail")

-- Flagstone path from hub to castle corridor
-- Path runs diagonally from ~(42, Y, -17) to ~(62, Y, -25)
local pathDir = (Vector3.new(62, 0, -25) - Vector3.new(42, 0, -17)).Unit
local pathLen = (Vector3.new(62, 0, -25) - Vector3.new(42, 0, -17)).Magnitude
local pathMid = (Vector3.new(42, 0, -17) + Vector3.new(62, 0, -25)) / 2

local path = Instance.new("Part")
path.Name = "FlagstonePath"
path.Size = Vector3.new(5, 0.15, pathLen)
path.CFrame = CFrame.lookAt(Vector3.new(pathMid.X, 0.15, pathMid.Z), Vector3.new(62, 0.15, -25))
path.Anchored = true
path.Material = Enum.Material.Slate
path.BrickColor = BrickColor.new("Dark stone grey")
path.Parent = trail

-- 4 stone wall sections along path
for i = 0, 3 do
    local t = (i + 0.5) / 4
    local wallPos = Vector3.new(42, 0, -17):Lerp(Vector3.new(62, 0, -25), t)
    local rightDir = pathDir:Cross(Vector3.new(0, 1, 0)).Unit

    local wall = Instance.new("Part")
    wall.Name = "PathWall" .. i
    wall.Size = Vector3.new(0.8, 4 + i, 4)
    wall.Position = Vector3.new(wallPos.X + rightDir.X * 4, 2 + i * 0.5, wallPos.Z + rightDir.Z * 4)
    wall.Anchored = true
    wall.Material = Enum.Material.Cobblestone
    wall.BrickColor = BrickColor.new("Dark stone grey")
    wall.Parent = trail
end

-- 6 iron lanterns on posts
for i = 0, 5 do
    local t = (i + 0.5) / 6
    local pos = Vector3.new(42, 0, -17):Lerp(Vector3.new(62, 0, -25), t)
    local side = (i % 2 == 0) and -3 or 3
    local rightDir = pathDir:Cross(Vector3.new(0, 1, 0)).Unit

    local post = Instance.new("Part")
    post.Name = "LanternPost"
    post.Size = Vector3.new(0.3, 4, 0.3)
    post.Position = Vector3.new(pos.X + rightDir.X * side, 2, pos.Z + rightDir.Z * side)
    post.Anchored = true
    post.Material = Enum.Material.Metal
    post.Color = Color3.fromRGB(50, 45, 40)
    post.Parent = trail

    local lantern = Instance.new("Part")
    lantern.Name = "Lantern"
    lantern.Size = Vector3.new(0.6, 0.8, 0.6)
    lantern.Position = post.Position + Vector3.new(0, 2.5, 0)
    lantern.Anchored = true
    lantern.Material = Enum.Material.Neon
    lantern.Color = Color3.fromRGB(255, 180, 80)
    lantern.Parent = trail

    local light = Instance.new("PointLight")
    light.Color = Color3.fromRGB(255, 170, 60)
    light.Brightness = 0.5
    light.Range = 8
    light.Parent = lantern
end

-- 2 heraldic banners
for i, t in {0.3, 0.7} do
    local pos = Vector3.new(42, 0, -17):Lerp(Vector3.new(62, 0, -25), t)
    local banner = Instance.new("Part")
    banner.Name = "HeraldBanner"
    banner.Size = Vector3.new(0.1, 5, 2)
    banner.Position = Vector3.new(pos.X, 5, pos.Z)
    banner.Anchored = true
    banner.Material = Enum.Material.Fabric
    banner.Color = i == 1 and Color3.fromRGB(150, 20, 30) or Color3.fromRGB(20, 40, 120)
    banner.Parent = trail
end

-- 2 guard statues
for i, t in {0.15, 0.85} do
    local pos = Vector3.new(42, 0, -17):Lerp(Vector3.new(62, 0, -25), t)
    local rightDir = pathDir:Cross(Vector3.new(0, 1, 0)).Unit
    local statueX = pos.X + rightDir.X * 3.5
    local statueZ = pos.Z + rightDir.Z * 3.5

    -- Pedestal
    local ped = Instance.new("Part")
    ped.Name = "StatuePedestal"
    ped.Size = Vector3.new(1.5, 1, 1.5)
    ped.Position = Vector3.new(statueX, 0.5, statueZ)
    ped.Anchored = true
    ped.Material = Enum.Material.Marble
    ped.Color = Color3.fromRGB(180, 175, 165)
    ped.Parent = trail

    -- Body
    local body = Instance.new("Part")
    body.Name = "StatueBody"
    body.Size = Vector3.new(1.2, 2.5, 0.8)
    body.Position = Vector3.new(statueX, 2.5, statueZ)
    body.Anchored = true
    body.Material = Enum.Material.Metal
    body.Color = Color3.fromRGB(140, 140, 150)
    body.Reflectance = 0.2
    body.Parent = trail

    -- Helmet
    local helmet = Instance.new("Part")
    helmet.Shape = Enum.PartType.Ball
    helmet.Size = Vector3.new(0.9, 1, 0.9)
    helmet.Position = Vector3.new(statueX, 4.2, statueZ)
    helmet.Anchored = true
    helmet.Material = Enum.Material.Metal
    helmet.Color = Color3.fromRGB(140, 140, 150)
    helmet.Reflectance = 0.2
    helmet.Parent = trail
end

print("[Trail] Castle trail built: path, 4 walls, 6 lanterns, 2 banners, 2 statues")
```

- [ ] **Step 2: Verify part count**

```lua
local count = 0
local trail = workspace:FindFirstChild("CastleTrail")
if trail then
    for _ in trail:GetDescendants() do count += 1 end
end
print("Castle trail parts:", count, "(budget: 50)")
```

---

### Task 6: Relocate Outfitter to Castle Trail Start

**Move "The Outfitter" from hub to the Castle trail entrance area.**

- [ ] **Step 1: Move outfitter model**

Same pattern as Task 3 — calculate offset, move all descendant BaseParts, reparent to CastleTrail folder.

Target position: near the stone wall entrance, approximately (38, 0, -17).

---

### Task 7: Range SpawnLocations + Respawn Logic

**Add transparent SpawnLocations in each range. Modify GameManager to set player.RespawnLocation when entering a range zone.**

- [ ] **Step 1: Create SpawnLocations**

```lua
-- execute_luau: Add range spawns
-- Greenwood spawn on deck
local gwSpawn = Instance.new("SpawnLocation")
gwSpawn.Name = "GreenwoodSpawn"
gwSpawn.Size = Vector3.new(6, 1, 6)
gwSpawn.Position = Vector3.new(0, 2.5, -3)
gwSpawn.Anchored = true
gwSpawn.Transparency = 1
gwSpawn.CanCollide = false
gwSpawn.Neutral = true
gwSpawn.Parent = workspace.SpawnLocations

-- Castle spawn on platform
local castleSpawn = Instance.new("SpawnLocation")
castleSpawn.Name = "CastleSpawn"
castleSpawn.Size = Vector3.new(6, 1, 6)
castleSpawn.Position = Vector3.new(85, 2.5, -5)
castleSpawn.Anchored = true
castleSpawn.Transparency = 1
castleSpawn.CanCollide = false
castleSpawn.Neutral = true
castleSpawn.Parent = workspace.SpawnLocations

print("[Respawn] Range SpawnLocations created")
```

- [ ] **Step 2: Add respawn logic to GameManager**

In `detectPlayerRange()` (already exists), add `player.RespawnLocation` assignment:

```
-- Find detectPlayerRange function and add after range detection:
-- After detecting range, set respawn location
local hubSpawn = workspace.SpawnLocations:FindFirstChild("FiringPlatformSpawn")
local gwSpawn = workspace.SpawnLocations:FindFirstChild("GreenwoodSpawn")
local castleSpawn = workspace.SpawnLocations:FindFirstChild("CastleSpawn")

-- In onFireArrow, after detectPlayerRange:
if rangeId == "greenwood" and gwSpawn then
    player.RespawnLocation = gwSpawn
elseif rangeId == "castle" and castleSpawn then
    player.RespawnLocation = castleSpawn
end
```

File: `game.ServerScriptService.GameManager`
Add respawn logic in `onFireArrow` after `detectPlayerRange` call, approximately line 627.

- [ ] **Step 3: Verify respawn works**

Playtest: walk to range, fire arrow (triggers round), die → should respawn at range, not hub.

---

### Task 8: Playtest Full Flow

- [ ] **Step 1: Start playtest, check initialization**

All scripts should initialize with zero errors. Both range targets registered.

- [ ] **Step 2: Walk hub → Greenwood trail**

Verify: sightline blocker hides the range from village. Trail feels progressively greener. Tavern visible along the trail.

- [ ] **Step 3: Walk hub → Castle trail**

Verify: stone wall hides the castle. Trail feels progressively medieval. Outfitter at trail start.

- [ ] **Step 4: Check part counts**

```lua
-- execute_luau: Total new parts
local total = 0
for _, folder in {"GreenwoodTrail", "CastleTrail"} do
    local f = workspace:FindFirstChild(folder)
    if f then
        for _ in f:GetDescendants() do total += 1 end
    end
end
print("Total new trail parts:", total, "(budget: 162)")
```

- [ ] **Step 5: Commit docs**

```bash
cd /home/jevenson/dev/_pet_projects/roblox
git add docs/ _ops/
git commit -m "docs: village trails phase 1 plan + spec v2"
git push
```
