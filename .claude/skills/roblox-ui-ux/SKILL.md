---
name: roblox-ui-ux
description: Use when building Roblox user interfaces - ScreenGui, Frame, TextLabel, TextButton, ImageLabel, UIListLayout, tweening, feedback effects, HUD design, shop UI, or any StarterGui work. Triggers on GUI, ScreenGui, Frame, UDim2, AnchorPoint, UICorner, TweenService, or layout mentions.
---

# Roblox UI/UX

## Overview

Build polished, responsive Roblox interfaces using native GUI components. Focus on clarity, feedback, and mobile-friendly layouts.

**Core principle:** Every action needs feedback. Players should never wonder "did that work?"

## When to Use

**Use for:**
- Building GUI screens (HUD, shop, menus)
- Layout systems (UIListLayout, UIGridLayout)
- Animations and tweening
- Feedback effects (popups, particles, sound)
- Mobile/desktop responsive design
- Accessibility considerations

**Skip for:** Game logic (use roblox-studio-expert), design decisions (use roblox-game-designer)

## GUI Hierarchy

```
StarterGui/
├── HUD/                    -- Always visible during gameplay
│   ├── ScoreDisplay
│   ├── XPBar
│   ├── StreakCounter
│   └── ChallengeTracker
├── ShopGui/                -- Modal overlay
│   ├── Background
│   ├── ItemGrid
│   └── CloseButton
├── ResultsGui/             -- End-of-round modal
└── DailyRewardGui/         -- Popup modal
```

### Gui Types

| Type | Use | Behavior |
|------|-----|----------|
| ScreenGui | 2D overlays | Always renders on screen |
| SurfaceGui | 3D surfaces | Renders on parts |
| BillboardGui | 3D floating | Always faces camera |

### ScreenGui Properties

```lua
local screenGui = Instance.new("ScreenGui")
screenGui.ResetOnSpawn = false        -- Persist across respawns
screenGui.IgnoreGuiInset = true       -- Use full screen (ignore topbar)
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling  -- Predictable layering
screenGui.DisplayOrder = 1            -- Higher = renders on top
```

## Core Components

### Frame (Container)

```lua
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0.3, 0, 0.4, 0)        -- 30% width, 40% height
frame.Position = UDim2.new(0.5, 0, 0.5, 0)    -- Center of screen
frame.AnchorPoint = Vector2.new(0.5, 0.5)     -- Anchor at center
frame.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
frame.BorderSizePixel = 0
```

### UDim2 Explained

```lua
UDim2.new(ScaleX, OffsetX, ScaleY, OffsetY)

-- Examples:
UDim2.new(1, 0, 0, 50)      -- Full width, 50px height
UDim2.new(0.5, -100, 0.5, 0) -- 50% + adjustment
UDim2.fromScale(0.5, 0.5)   -- Shorthand for scale-only
UDim2.fromOffset(200, 100)  -- Shorthand for pixel-only
```

### AnchorPoint

```lua
-- AnchorPoint determines what part of the element Position refers to
frame.AnchorPoint = Vector2.new(0, 0)     -- Top-left (default)
frame.AnchorPoint = Vector2.new(0.5, 0.5) -- Center
frame.AnchorPoint = Vector2.new(1, 1)     -- Bottom-right

-- Common pattern: Center an element
frame.Position = UDim2.fromScale(0.5, 0.5)
frame.AnchorPoint = Vector2.new(0.5, 0.5)
```

### TextLabel

```lua
local label = Instance.new("TextLabel")
label.Text = "Score: 0"
label.Font = Enum.Font.GothamBold
label.TextSize = 24
label.TextColor3 = Color3.new(1, 1, 1)
label.TextXAlignment = Enum.TextXAlignment.Left
label.TextYAlignment = Enum.TextYAlignment.Center
label.BackgroundTransparency = 1  -- No background
label.TextScaled = false          -- Fixed size (prefer over TextScaled)
```

### TextButton

```lua
local button = Instance.new("TextButton")
button.Text = "Play"
button.Font = Enum.Font.GothamBold
button.TextSize = 20
button.TextColor3 = Color3.new(1, 1, 1)
button.BackgroundColor3 = Color3.fromRGB(0, 170, 127)
button.AutoButtonColor = true     -- Built-in hover/press states

button.Activated:Connect(function()
    -- Activated fires for clicks AND touch
    print("Button pressed!")
end)
```

### ImageLabel / ImageButton

```lua
local image = Instance.new("ImageLabel")
image.Image = "rbxassetid://123456789"  -- Asset ID
image.ScaleType = Enum.ScaleType.Fit    -- Fit, Crop, Stretch, Tile
image.BackgroundTransparency = 1
```

## Layout Components

### UIListLayout (Vertical/Horizontal Lists)

```lua
local layout = Instance.new("UIListLayout")
layout.FillDirection = Enum.FillDirection.Vertical
layout.HorizontalAlignment = Enum.HorizontalAlignment.Center
layout.VerticalAlignment = Enum.VerticalAlignment.Top
layout.Padding = UDim.new(0, 10)  -- 10px between items
layout.SortOrder = Enum.SortOrder.LayoutOrder
layout.Parent = containerFrame

-- Children are sorted by LayoutOrder property
child1.LayoutOrder = 1
child2.LayoutOrder = 2
```

### UIGridLayout (Grid of Items)

```lua
local grid = Instance.new("UIGridLayout")
grid.CellSize = UDim2.fromOffset(100, 100)  -- Each cell 100x100px
grid.CellPadding = UDim2.fromOffset(10, 10)
grid.FillDirection = Enum.FillDirection.Horizontal
grid.FillDirectionMaxCells = 4  -- Max 4 per row
grid.Parent = containerFrame
```

### UIAspectRatioConstraint

```lua
-- Keep element square regardless of parent size
local aspect = Instance.new("UIAspectRatioConstraint")
aspect.AspectRatio = 1  -- Width:Height ratio
aspect.AspectType = Enum.AspectType.FitWithinMaxSize
aspect.Parent = frame
```

### UIPadding

```lua
local padding = Instance.new("UIPadding")
padding.PaddingTop = UDim.new(0, 20)
padding.PaddingBottom = UDim.new(0, 20)
padding.PaddingLeft = UDim.new(0, 20)
padding.PaddingRight = UDim.new(0, 20)
padding.Parent = frame
```

### UICorner (Rounded Corners)

```lua
local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 8)  -- 8px radius
corner.Parent = frame
```

### UIStroke (Outline)

```lua
local stroke = Instance.new("UIStroke")
stroke.Color = Color3.new(1, 1, 1)
stroke.Thickness = 2
stroke.Transparency = 0.5
stroke.Parent = frame
```

### UIGradient

```lua
local gradient = Instance.new("UIGradient")
gradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(50, 50, 80)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(30, 30, 50))
})
gradient.Rotation = 90  -- Vertical gradient
gradient.Parent = frame
```

## Animation with TweenService

### Basic Tween

```lua
local TweenService = game:GetService("TweenService")

local tweenInfo = TweenInfo.new(
    0.3,                          -- Duration
    Enum.EasingStyle.Quad,        -- Easing style
    Enum.EasingDirection.Out,     -- Easing direction
    0,                            -- Repeat count (0 = no repeat)
    false,                        -- Reverses
    0                             -- Delay
)

local tween = TweenService:Create(frame, tweenInfo, {
    Position = UDim2.fromScale(0.5, 0.4),
    BackgroundTransparency = 0
})

tween:Play()
```

### Common Easing Styles

| Style | Use For |
|-------|---------|
| Quad | General UI transitions |
| Back | Bouncy entrance/exit |
| Elastic | Playful, springy motion |
| Sine | Smooth, natural motion |
| Linear | Progress bars, timers |

### Popup Pattern

```lua
local function showPopup(gui)
    gui.Visible = true
    gui.Position = UDim2.fromScale(0.5, 0.6)  -- Start below center
    gui.BackgroundTransparency = 1

    local tween = TweenService:Create(gui, TweenInfo.new(0.3, Enum.EasingStyle.Back), {
        Position = UDim2.fromScale(0.5, 0.5),
        BackgroundTransparency = 0
    })
    tween:Play()
end

local function hidePopup(gui)
    local tween = TweenService:Create(gui, TweenInfo.new(0.2, Enum.EasingStyle.Quad), {
        Position = UDim2.fromScale(0.5, 0.6),
        BackgroundTransparency = 1
    })
    tween:Play()
    tween.Completed:Connect(function()
        gui.Visible = false
    end)
end
```

### Button Feedback

```lua
local function setupButtonFeedback(button)
    local originalSize = button.Size

    button.MouseEnter:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.1), {
            Size = UDim2.new(
                originalSize.X.Scale * 1.05, originalSize.X.Offset,
                originalSize.Y.Scale * 1.05, originalSize.Y.Offset
            )
        }):Play()
    end)

    button.MouseLeave:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.1), {
            Size = originalSize
        }):Play()
    end)
end
```

## Feedback Patterns

### Score Popup

```lua
local function showScorePopup(score, worldPosition)
    local billboardGui = Instance.new("BillboardGui")
    billboardGui.Size = UDim2.fromOffset(100, 50)
    billboardGui.StudsOffset = Vector3.new(0, 2, 0)
    billboardGui.Adornee = workspace.Terrain  -- Or a part
    billboardGui.AlwaysOnTop = true

    local label = Instance.new("TextLabel")
    label.Text = "+" .. score
    label.Font = Enum.Font.GothamBold
    label.TextSize = 32
    label.TextColor3 = score >= 10 and Color3.new(1, 0.8, 0) or Color3.new(1, 1, 1)
    label.BackgroundTransparency = 1
    label.Size = UDim2.fromScale(1, 1)
    label.Parent = billboardGui

    -- Animate upward and fade
    local tween = TweenService:Create(billboardGui, TweenInfo.new(1), {
        StudsOffset = Vector3.new(0, 5, 0)
    })
    local fadeTween = TweenService:Create(label, TweenInfo.new(1), {
        TextTransparency = 1
    })

    tween:Play()
    fadeTween:Play()

    task.delay(1, function()
        billboardGui:Destroy()
    end)
end
```

### Progress Bar

```lua
local function updateProgressBar(bar, fill, current, max)
    local percent = math.clamp(current / max, 0, 1)

    TweenService:Create(fill, TweenInfo.new(0.3, Enum.EasingStyle.Quad), {
        Size = UDim2.new(percent, 0, 1, 0)
    }):Play()
end
```

### Screen Shake (Camera)

```lua
local function screenShake(intensity, duration)
    local camera = workspace.CurrentCamera
    local originalCFrame = camera.CFrame

    local startTime = tick()
    local connection
    connection = game:GetService("RunService").RenderStepped:Connect(function()
        local elapsed = tick() - startTime
        if elapsed > duration then
            connection:Disconnect()
            return
        end

        local decay = 1 - (elapsed / duration)
        local offset = Vector3.new(
            (math.random() - 0.5) * intensity * decay,
            (math.random() - 0.5) * intensity * decay,
            0
        )
        camera.CFrame = originalCFrame * CFrame.new(offset)
    end)
end
```

## Responsive Design

### Device Detection

```lua
local UserInputService = game:GetService("UserInputService")

local function isMobile()
    return UserInputService.TouchEnabled and not UserInputService.KeyboardEnabled
end

local function isTablet()
    local viewport = workspace.CurrentCamera.ViewportSize
    return isMobile() and math.min(viewport.X, viewport.Y) > 600
end
```

### Adaptive Sizing

```lua
-- Scale text based on screen size
local function getResponsiveTextSize(baseSize)
    local viewport = workspace.CurrentCamera.ViewportSize
    local scale = math.clamp(viewport.Y / 1080, 0.7, 1.3)
    return math.floor(baseSize * scale)
end

-- Adjust layout for mobile
local function setupResponsiveLayout(container, mobileColumns, desktopColumns)
    local grid = container:FindFirstChildOfClass("UIGridLayout")
    if grid then
        grid.FillDirectionMaxCells = isMobile() and mobileColumns or desktopColumns
    end
end
```

### Safe Area (Notch/Island)

```lua
local GuiService = game:GetService("GuiService")

-- Get safe area insets
local insets = GuiService:GetGuiInset()
-- Returns (topInset, bottomInset) as Vector2

-- Apply to top-level container
mainFrame.Position = UDim2.new(0, 0, 0, insets.Y)
```

## Common UI Patterns

### Modal Overlay

```lua
-- Dark background that blocks input
local overlay = Instance.new("Frame")
overlay.Size = UDim2.fromScale(1, 1)
overlay.Position = UDim2.fromScale(0, 0)
overlay.BackgroundColor3 = Color3.new(0, 0, 0)
overlay.BackgroundTransparency = 0.5
overlay.ZIndex = 10

-- Click overlay to close
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.fromScale(1, 1)
closeButton.BackgroundTransparency = 1
closeButton.Text = ""
closeButton.Parent = overlay
closeButton.Activated:Connect(function()
    hidePopup(modalContent)
    overlay.Visible = false
end)
```

### Tab Navigation

```lua
local function setupTabs(tabContainer, contentContainer, tabs)
    for i, tabData in ipairs(tabs) do
        local button = tabContainer:FindFirstChild(tabData.name .. "Tab")
        local content = contentContainer:FindFirstChild(tabData.name .. "Content")

        button.Activated:Connect(function()
            -- Hide all content
            for _, child in ipairs(contentContainer:GetChildren()) do
                if child:IsA("Frame") then
                    child.Visible = false
                end
            end
            -- Show selected
            content.Visible = true

            -- Update tab visuals
            for _, tab in ipairs(tabContainer:GetChildren()) do
                if tab:IsA("TextButton") then
                    tab.BackgroundColor3 = Color3.fromRGB(50, 50, 60)
                end
            end
            button.BackgroundColor3 = Color3.fromRGB(80, 80, 100)
        end)
    end
end
```

### Scrolling Frame

```lua
local scrollFrame = Instance.new("ScrollingFrame")
scrollFrame.Size = UDim2.fromScale(0.8, 0.6)
scrollFrame.CanvasSize = UDim2.fromScale(0, 0)  -- Auto-calculated
scrollFrame.AutomaticCanvasSize = Enum.AutomaticSize.Y
scrollFrame.ScrollBarThickness = 6
scrollFrame.ScrollBarImageColor3 = Color3.fromRGB(100, 100, 100)
scrollFrame.BorderSizePixel = 0

-- Add UIListLayout for auto-sizing content
local layout = Instance.new("UIListLayout")
layout.Parent = scrollFrame
```

## Accessibility

### Color Contrast

| Use | Background | Text | Ratio |
|-----|------------|------|-------|
| Primary | #1E1E28 | #FFFFFF | 15:1 |
| Secondary | #2A2A3A | #E0E0E0 | 10:1 |
| Accent | #00AA7F | #FFFFFF | 4.5:1 |
| Error | #FF4444 | #FFFFFF | 4.5:1 |

### Touch Targets

- Minimum button size: 44x44 pixels
- Adequate spacing between interactive elements
- Visual feedback on all interactions

### Text Legibility

- Minimum body text: 14px (scaled)
- Important info: 18px+
- Avoid pure white on pure black (use #E0E0E0 on #1E1E28)

## Quick Reference

### Z-Index Layering

| Layer | ZIndex | Content |
|-------|--------|---------|
| Background | 1 | Ambient UI, decorations |
| HUD | 5 | Score, XP bar, minimap |
| Menus | 10 | Shop, inventory, settings |
| Modals | 15 | Popups, confirmations |
| Tooltips | 20 | Hover info |
| System | 25 | Loading, errors |

### Standard Sizes

| Element | Size |
|---------|------|
| Button height | 44-56px |
| Icon | 24-32px |
| Modal width | 60-80% of screen |
| Padding | 12-20px |
| Corner radius | 4-12px |

## UI Checklist

Before shipping any UI:

- [ ] Works on mobile (touch targets, no hover-only)
- [ ] Scales on different screen sizes
- [ ] Has feedback on all interactions
- [ ] Animations are 0.1-0.3s (not sluggish)
- [ ] Text is legible at all sizes
- [ ] Close/back buttons are obvious
- [ ] Loading states exist
- [ ] Error states are handled
