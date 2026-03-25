# MCP Tools Reference

Detailed reference for robloxstudio-mcp tools. See SKILL.md for workflow guidance.

## Inspection Tools

### get_project_structure

Get full hierarchy tree. Use `maxDepth` for large projects.

```
get_project_structure(path="game.ServerScriptService", maxDepth=5, scriptsOnly=true)
```

**Parameters:**
- `path` - Root path (default: workspace root)
- `maxDepth` - Traversal depth (default: 3)
- `scriptsOnly` - Only show scripts (default: false)

### get_script_source

Read script content with line numbers.

```
get_script_source(instancePath="game.ServerScriptService.GameManager")
```

Returns `source` (raw) and `numberedSource` (with line numbers).

For large scripts, use `startLine`/`endLine`:
```
get_script_source(instancePath="...", startLine=50, endLine=100)
```

### grep_scripts

Ripgrep-style search across all scripts.

```
grep_scripts(
    pattern="FireServer",
    path="game.ReplicatedStorage",
    contextLines=2,
    maxResults=50
)
```

**Parameters:**
- `pattern` - Literal string or Lua pattern (if `usePattern=true`)
- `path` - Subtree to search
- `contextLines` - Lines before/after match (like `rg -C`)
- `filesOnly` - Return paths only, not content
- `classFilter` - "Script", "LocalScript", or "ModuleScript"
- `caseSensitive` - Default false

### search_objects

Find instances by name, class, or property.

```
search_objects(query="Arrow", searchType="name")
search_objects(query="RemoteEvent", searchType="class")
search_objects(query="Transparency", searchType="property", propertyName="Transparency")
```

### get_instance_properties

All properties of an instance.

```
get_instance_properties(instancePath="game.Workspace.Targets.Target1")
```

Use `excludeSource=true` for scripts to skip source (returns line count instead).

### get_instance_children

Direct children with class types.

```
get_instance_children(instancePath="game.ReplicatedStorage.Remotes")
```

## Modification Tools

### set_script_source

Replace entire script. Use for new scripts or full rewrites.

```
set_script_source(
    instancePath="game.ServerScriptService.GameManager",
    source="-- Full script content here\nlocal Players = game:GetService('Players')\n..."
)
```

### edit_script_lines

Replace specific line range (1-indexed, inclusive).

```
edit_script_lines(
    instancePath="game.ServerScriptService.GameManager",
    startLine=15,
    endLine=20,
    newContent="-- New content for lines 15-20\nlocal newVar = 42"
)
```

**IMPORTANT:** Always use `get_script_source` first to see line numbers.

### insert_script_lines

Insert after a line (0 = beginning).

```
insert_script_lines(
    instancePath="game.ServerScriptService.GameManager",
    afterLine=10,
    newContent="-- Inserted after line 10\nlocal newFunction = function() end"
)
```

### delete_script_lines

Remove line range.

```
delete_script_lines(
    instancePath="game.ServerScriptService.GameManager",
    startLine=25,
    endLine=30
)
```

### create_object

Create new instance with optional properties.

```
create_object(
    className="RemoteEvent",
    parent="game.ReplicatedStorage.Remotes",
    name="NewEvent"
)

create_object(
    className="Script",
    parent="game.ServerScriptService",
    name="NewManager",
    properties={"Source": "-- Initial content"}
)
```

### set_property

Set single property.

```
set_property(
    instancePath="game.Workspace.Part1",
    propertyName="Transparency",
    propertyValue=0.5
)
```

**Complex types:**
```
-- Vector3
set_property(path, "Position", {"X": 0, "Y": 10, "Z": 0})

-- Color3
set_property(path, "Color", {"R": 1, "G": 0, "B": 0})

-- CFrame (position + orientation)
set_property(path, "CFrame", {
    "Position": {"X": 0, "Y": 5, "Z": 0},
    "Orientation": {"X": 0, "Y": 45, "Z": 0}
})
```

### mass_set_property

Batch property updates.

```
mass_set_property(
    paths=["game.Workspace.Part1", "game.Workspace.Part2", "game.Workspace.Part3"],
    propertyName="Anchored",
    propertyValue=true
)
```

### delete_object

Remove instance.

```
delete_object(instancePath="game.Workspace.OldPart")
```

## Procedural Build Tools

### generate_build

Create builds procedurally with JS code.

```
generate_build(
    id="medieval/tower_01",
    style="medieval",
    palette={
        "s": ["Dark stone grey", "Cobblestone"],
        "w": ["Brown", "WoodPlanks"]
    },
    code="""
room(0,0,0, 6,8,6, "s", "s", "s")
roof(0,8,0, 6,6, "flat", "s")
part(0,4,-3, 1.5,2,0.2, "w")
"""
)
```

**Available primitives in code:**

High-level:
- `room(x,y,z, w,h,d, wallKey, floorKey?, ceilKey?, wallThickness?)`
- `roof(x,y,z, w,d, style, key, overhang?)` - styles: "flat", "gable", "hip"
- `stairs(x1,y1,z1, x2,y2,z2, width, key)`
- `column(x,y,z, height, radius, key, capKey?)`
- `pew(x,y,z, w,d, seatKey, legKey?)`
- `arch(x,y,z, w,h, thickness, key, segments?)`
- `fence(x1,z1, x2,z2, y, key, postSpacing?)`

Basic:
- `part(x,y,z, sx,sy,sz, key, shape?, transparency?)`
- `rpart(x,y,z, sx,sy,sz, rx,ry,rz, key, shape?, transparency?)`
- `wall(x1,z1, x2,z2, height, thickness, key)`
- `floor(x1,z1, x2,z2, y, thickness, key)`
- `fill(x1,y1,z1, x2,y2,z2, key, [ux,uy,uz]?)`
- `beam(x1,y1,z1, x2,y2,z2, thickness, key)`

Repetition:
- `row(x,y,z, count, spacingX, spacingZ, fn(i,cx,cy,cz))`
- `grid(x,y,z, countX, countZ, spacingX, spacingZ, fn(ix,iz,cx,cy,cz))`

Shapes: Block (default), Wedge, Cylinder, Ball, CornerWedge

### import_build

Place a saved build into Studio.

```
import_build(
    buildData="medieval/tower_01",  -- Library ID string
    targetPath="game.Workspace.Builds",
    position=[100, 0, 50]
)
```

### import_scene

Place multiple builds at once.

```
import_scene(
    sceneData={
        "models": {
            "T": "medieval/tower_01",
            "W": "medieval/wall_section"
        },
        "place": [
            {"modelKey": "T", "position": [0, 0, 0]},
            {"modelKey": "W", "position": [10, 0, 0], "rotation": [0, 90, 0]},
            {"modelKey": "W", "position": [-10, 0, 0], "rotation": [0, 90, 0]}
        ]
    },
    targetPath="game.Workspace"
)
```

### list_library

Browse saved builds.

```
list_library()
list_library(style="medieval")
```

### get_build

Retrieve build for editing.

```
get_build(id="medieval/tower_01")
```

**Important:** When editing existing builds, ALWAYS get_build first, make targeted changes, then generate_build with modified code.

## Testing Tools

### start_playtest

Begin playtest session.

```
start_playtest(mode="play")   -- Full client simulation
start_playtest(mode="run")    -- Server only (faster)
```

### get_playtest_output

Poll output without stopping.

```
get_playtest_output()
```

Returns `isRunning` and `messages` array with print/warn/error.

### stop_playtest

End session and get all output.

```
stop_playtest()
```

### execute_luau

Run arbitrary Luau in plugin context.

```
execute_luau(code="""
local count = 0
for _, v in ipairs(workspace:GetDescendants()) do
    if v:IsA("BasePart") then count += 1 end
end
print("Total parts:", count)
return count
""")
```

**Use for:** Quick queries, validation, one-off operations.

## Attribute & Tag Tools

### get_attributes / set_attribute

```
get_attributes(instancePath="game.Workspace.Target1")

set_attribute(
    instancePath="game.Workspace.Target1",
    attributeName="ScoreValue",
    attributeValue=10
)
```

### get_tags / add_tag / remove_tag

```
get_tags(instancePath="game.Workspace.Target1")
add_tag(instancePath="game.Workspace.Target1", tagName="Scoreable")
remove_tag(instancePath="game.Workspace.Target1", tagName="Scoreable")
```

### get_tagged

Find all instances with a tag.

```
get_tagged(tagName="Scoreable")
```

## Asset Tools

### search_assets

Search Creator Store.

```
search_assets(
    assetType="Model",
    query="medieval castle",
    maxResults=10,
    verifiedCreatorsOnly=true
)
```

Asset types: Audio, Model, Decal, Plugin, MeshPart, Video, FontFamily

### insert_asset

Insert asset into Studio.

```
insert_asset(
    assetId=12345678,
    parentPath="game.Workspace",
    position={"x": 0, "y": 10, "z": 0}
)
```

### preview_asset

Inspect asset without inserting.

```
preview_asset(assetId=12345678)
```

## Utility Tools

### undo / redo

```
undo()
redo()
```

### capture_screenshot

Capture viewport (requires EditableImage API enabled).

```
capture_screenshot()
```

### search_materials

Find MaterialVariant instances.

```
search_materials(query="stone")
```

Use results in palette: `["Color", "BaseMaterial", "VariantName"]`
