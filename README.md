# RGUI — The ImGui for Roblox

<img width="359" height="222" alt="image" src="https://github.com/user-attachments/assets/b32e293c-13e1-4194-bce7-6e0aaf8e0bc5" />

# Demo Window
```lua
local RGui = loadstring(game:HttpGet("YOUR_RAW_LINK_HERE"))()

local win = RGui.new("Demo")

local Main = win:AddTab("Main")

Main:AddSection("Example")

Main:AddButton("Print Hello", function()
    print("Hello!")
end)

Main:AddCheckbox("Enabled", false, function(state)
    print(state)
end)

Main:AddSlider("WalkSpeed", 16, 100, 16, function(value)
    print(value)
end)
```

# Installation

```lua
local RGui = loadstring(game:HttpGet("YOUR_RAW_LINK_HERE"))()
```

```lua
local RGui = loadstring(game:HttpGet(
    "rawlinkHere"
))()
```


Options:

Position: UDim2 (e.g., UDim2.new(0.5, -200, 0.3, 0))

Size: UDim2 (e.g., UDim2.new(0, 400, 0, 300))

Icon: string – Roblox asset ID for a title bar icon.

# Creating a Window

```lua
local win = RGui.new("My Tool", nil, {
    Position = UDim2.new(0, 100, 0, 50),
    Size = UDim2.new(0, 500, 0, 400),
    Icon = "rbxassetid://1234567890" -- Optional
})
```

# Toggle the GUI:

```lua
win._screen.Enabled = false  -- hide
win._screen.Enabled = true   -- show
```
# Key System

A built‑in two‑column key verification window with service selection and copy buttons.

```lua
win:CreateKeySystem({
    ScriptTitle = "My Script",          -- optional
    Icon = "rbxassetid://12345",        -- optional title bar icon
    Services = {
        ["Linkvertise"] = {
            CopyLink = "https://linkvertise.com/yourkey",
            Validate = function(key) return key == "LV-ABC" end
        },
        ["Direct Key"] = {
            CopyKey = "SECRET123",
            Validate = function(key) return key == "SECRET123" end
        }
    },
    Description = "Enter your premium key to continue.",
    Callback = function(service, key)
        win._screen.Enabled = true   -- show main GUI after valid key
    end
})
```

<img width="427" height="197" alt="image" src="https://github.com/user-attachments/assets/f17943d2-8b38-43f0-a299-1df55fc55f6b" />

# Tabs
Add tabs to organise your UI. Each tab can have an optional icon.

```lua
local combat = win:AddTab("Combat")
local settings = win:AddTab("Settings", "rbxassetid://111")   -- icon
```

# Sections
Group related controls under a labelled section.

```lua
tab:AddSection("Aimbot")
```

# Labels
Display static text (supports rich text).

```lua
tab:AddLabel("Welcome to RGUI!", Color3.fromRGB(255, 200, 200))
```
# Buttons
A clickable button. Can optionally include an icon and even a custom colour (but the library will warn you for breaking theme consistency).


```lua
tab:AddButton("Click me", function()
    print("Clicked!")
end)
```

-- With an icon
```lua
tab:AddButton("Save", callback, "rbxassetid://222")
```
```lua
-- Risky custom colour (triggers a warning notification)
tab:AddButton("Danger", callback, { Color = Color3.fromRGB(255, 0, 0) })
```
# Checkboxes
Toggle settings on/off.

```lua
tab:AddCheckbox("Enable Aimbot", false, function(state)
    print("Aimbot:", state)
end)
```

-- Custom background colour
```lua
tab:AddCheckbox("Risky", true, callback, { Color = Color3.fromRGB(0, 255, 0) })
```
# Sliders
Numeric adjustment with a draggable handle.
(No decimals allowed; value is always an integer.)

```lua
tab:AddSlider("Volume", 0, 100, 50, function(value)
    print(value)
end)
```
You can also pass a custom track colour via options:

```lua
    tab:AddSlider("Speed", 16, 250, 16, callback, { Color = Color3.fromRGB(255, 100, 100) })
```

# Dropdowns & Variants

Standard Dropdown
```lua
tab:AddDropdown("Mode", {"Easy", "Hard", "Extreme"}, "Easy", function(selected)
    print(selected)
end)
```
# Searchable Dropdown
Type to filter through many options.

```lua
tab:AddSearchableDropdown("Fruit", {"Apple", "Banana", "Cherry", "Date"}, "Apple", function(selected)
    print(selected)
end)
```
# Multi‑Select Dropdown
Select multiple items. Header shows selected count.

```lua
tab:AddMultiSelectDropdown("Toppings", {"Cheese", "Tomato", "Olives"}, {"Cheese"}, function(selected)
    print(table.concat(selected, ", "))
end)
```
# Multi‑Select + Searchable Dropdown
Filter the list and pick many items.

```lua
tab:AddMultiSelectSearchableDropdown("Colors", {"Red", "Green", "Blue"}, {"Blue"}, function(selected)
    print(table.concat(selected, ", "))
end)
```
# Color Picker
Expandable colour picker with R/G/B sliders and a live preview.

```lua
tab:AddColorPicker("Accent", Color3.fromRGB(255, 255, 255), function(color)
    print(color)
end)
```
# Text Inputs
A single‑line text box with a label.

```lua
tab:AddTextBox("Username", "Enter name", "", function(text)
    print("Input:", text)
end)
```

# Keybind Picker
Listen for keyboard keys or mouse buttons (Mouse1–Mouse2).
Click the "Bind" button, then press the desired key/mouse button.

```lua
tab:AddKeybindPicker("Fly Key", Enum.KeyCode.F, function(key)
    print("Key set to:", key)   -- e.g., "F", "Mouse1"
end)
```

```lua
-- Start with a mouse button

tab:AddKeybindPicker("Aim Key", "Mouse1", function(key) end)
```

Returns an object with :GetKey() and :SetKey() for runtime updates.

# Code Editor
A multi‑line, scrollable text area with monospaced font – perfect for Lua code or large text blocks.

```lua
tab:AddCodeEditor("Script", "print('Hello')", "", function(code)
    print("Code changed:", code)
end)
```

# Graphs
Real‑time Catmull‑Rom spline graphs that are smooth and performant.

```lua
local graph = tab:AddGraph("FPS", 60, {
    LineColor = Color3.fromRGB(0, 255, 0),
    YMin = 0,
    YMax = 200
})

-- Push new values regularly
task.spawn(function()
    while task.wait(0.2) do
        graph:Push(fpsValue)
    end
end)
```

Example: In‑Game Health Monitor

```lua
local Players = game:GetService("Players")
local player = Players.LocalPlayer

local healthGraph = tab:AddGraph("Health", 60, {
    YMin = 0,
    YMax = 100,
    LineColor = Color3.fromRGB(0, 255, 0)
})

task.spawn(function()
    while task.wait(0.2) do
        local character = player.Character
        local humanoid = character and character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            healthGraph:Push(humanoid.Health)
        end
    end
end)
```
<img width="400" height="237" alt="image" src="https://github.com/user-attachments/assets/31240b47-104a-41a2-bdf6-fd297d686881" />

# Custom Themes
You can completely restyle the UI with a theme table. Any missing keys will fall back to the default blue theme.

```lua
local PinkTheme = {
    WindowBg      = Color3.fromRGB(17, 14, 20),
    TitleBg       = Color3.fromRGB(22, 18, 27),
    Border        = Color3.fromRGB(56, 42, 66),
    Text          = Color3.fromRGB(245, 242, 248),
    SubText       = Color3.fromRGB(168, 160, 178),
    Accent        = Color3.fromRGB(255, 92, 176),
    AccentHover   = Color3.fromRGB(255, 122, 194),
    FrameBg       = Color3.fromRGB(24, 20, 30),
    FrameBgHover  = Color3.fromRGB(31, 26, 38),
    CheckOff      = Color3.fromRGB(22, 18, 27),
    CheckOn       = Color3.fromRGB(255, 92, 176),
    SliderTrack   = Color3.fromRGB(45, 38, 54),
    SliderFill    = Color3.fromRGB(255, 92, 176),
    TabBarBg      = Color3.fromRGB(22, 18, 27),
    TabNormal     = Color3.fromRGB(22, 18, 27),
    TabNormalText = Color3.fromRGB(168, 160, 178),
    TabActive     = Color3.fromRGB(33, 27, 41),
    TabActiveText = Color3.fromRGB(255, 92, 176),
    GraphBg       = Color3.fromRGB(20, 17, 24),
    GraphLine     = Color3.fromRGB(255, 116, 189),
}
```
Then pass it to the window:

```lua
local win = RGui.new("Pink GUI", PinkTheme)
```
Theme Generator: Use this handy tool to generate your own themes visually.
ThemeGenerator.html

<img width="406" height="304" alt="image" src="https://github.com/user-attachments/assets/50056d69-c8e7-4a46-91d6-5f347a2853f1" />

# Watermarks
A draggable, title‑bar‑styled watermark that stays on screen.

Static

```lua
local wm = win:CreateWatermark("My Script", {
    TextColor = Color3.fromRGB(255, 255, 255),
    TextSize = 14,
    Position = UDim2.new(0, 2, 0, 2)
})
```

# Dynamic (Update Method)
The Update() method lets you change the text (or any option) on the fly. Perfect for FPS counters!

```lua
local wm = win:CreateWatermark("Loading...", {
    Icon = "rbxassetid://111",
    TextColor = Color3.fromRGB(255, 255, 255),
    TextSize = 14,
    Position = UDim2.new(0, 10, 0, 10)
})

task.spawn(function()
    while task.wait(0.5) do
        local ping = game.Players.LocalPlayer:GetNetworkPing() * 1000
        wm:Update(string.format("FPS: %d  Ping: %.0f ms", fps, ping))
    end
end)
https://github.com/user-attachments/assets/c79fa482-4802-4900-aa73-d63d67f9d1f2
```
# Notifications
Stacking toast notifications in the bottom‑right corner.

```lua
win:Notify("Success", "Key verified!", 4)  -- duration in seconds
```
-- Custom accent colour
```lua
win:Notify("Warning", "Something went wrong!", 3, {
    Color = Color3.fromRGB(255, 255, 0)
})
```
# Configuration API
Save and load settings easily with RGui.Config.

```lua
local config = RGui.Config.new("MyScriptConfig")
config:Load()   -- load saved data from local storage

local tab = win:AddTab("Settings")
config:BindCheckbox(tab, "EnableESP", "ESP", false)
-- (more bindings can be added)

-- Save on window close
-- You can hook into the close button or use win:Destroy() to auto‑save
```
# Find Me On Rscripts
<a href="https://rscripts.net/user/GoatedCitizen" target="_blank"><img alt="GoatedCitizen on Rscripts" loading="lazy" width="360" height="132" src="https://rscripts.net/api/embed/user/GoatedCitizen?theme=dark" /></a>
