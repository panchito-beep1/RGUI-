# RGUI The Imgui For Roblox

# Demo Window

```lua
local RGui = loadstring(game:HttpGet(""))()

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
local RGui = loadstring(game:HttpGet(
    "Link To Gui",
    true
))()
```
# How to create a window

```lua
local win = RGui.new("Example Window")
```

> You Can Toggle the GUI like this
```lua
win._screen.Enabled = false
```

```lua
win._screen.Enabled = true
```

# How to create a KeySystem

```lua
win:CreateKeySystem({
    ScriptTitle = "Example Key System",
    Services = {
        ["Directkey"] = { CopyLink = "Secret Key", Validate = function(k) return k == "Secret Key" end },
    },
    Description = "Example Key system The Key Is Secret Key",
    Callback = function(service, key)
        --Your Callback/Function
    end
```
<img width="427" height="197" alt="image" src="https://github.com/user-attachments/assets/08a0e539-41e9-495b-925f-1c4cae10a291" />

# How to create Tabs

```lua
local Example    = win:AddTab("tab")
```

# How to create Sections

```lua
tab:AddSection("Selection")
```

# How to create Labels

```lua
tab:AddLabel("Example Label")
```

# How to create Buttons

```lua
tab:AddButton("Example Button", function()
    print("Button clicked")
    --Your Function
end)
```

# How to create Checkboxes

```lua

tab:AddCheckbox("Example Checkbox", false, function(state)
    print(state)
    --your function
end)
```

# How to create Sliders

```lua

tab:AddSlider("Example Slider", 0, 100, 50, function(value) -- 0 represents the minimum, 100 the maximum, and 50 the start position. Note, don't use decimals
    print(value)
end)
```

# How to create DropDowns and their variants

> Normal Dropdown

```lua

tab:AddDropdown(
    "Example Dropdown",
    {"Option 1", "Option 2", "Option 3"},
    "Option 1",
    function(selected)
        print(selected)
        --your Function
    end
)
```
> Searchable Dropdown
```lua
tab:AddSearchableDropdown(
    "Searchable Dropdown",
    {"Apple", "Banana", "Cherry"},
    "Apple",
    function(selected)
        print(selected)
    end
)
```

> Multiselect + Searchable Dropdown
```lua
tab:AddMultiSelectSearchableDropdown(
    "Multi Select",
    {"Red", "Green", "Blue"},
    {"Blue"},
    function(selected)
        print(table.concat(selected, ", "))
    end
)
```

# Color Pickers

```lua
tab:AddColorPicker(
    "Example Color",
    Color3.fromRGB(255, 255, 255),
    function(color)
        print(color)
    end
)
```

# Text Inputs

```lua
tab:AddTextBox("Search", "Search items...", "", function(txt) print("Search:", txt) end)
```

# Graphs 🚧WARNING this is a Beta Feature may have errors + not work as expected

```lua
local graph = tab:AddGraph("Example Graph", 60, {
    YMin = 0,
    YMax = 100,
    LineColor = Color3.fromRGB(0, 170, 255) -Color Customization
})

local value = 50
local direction = 1

task.spawn(function()
    while task.wait(0.15) do
    --Value For the Graph
        value += math.random(2, 8) * direction

        -- Set Limits
        if value >= 100 then
            value = 100
            direction = -1
        elseif value <= 0 then
            value = 0
            direction = 1
        end

        graph:Push(value)
    end
end)
```

> Example Using an In-Game Value

```lua
local Players = game:GetService("Players")
local player = Players.LocalPlayer

local graph = tab:AddGraph("Health", 60, {
    YMin = 0,
    YMax = 100,
    LineColor = Color3.fromRGB(0, 255, 0)
})

task.spawn(function()
    while task.wait(0.2) do
        local character = player.Character
        local humanoid = character and character:FindFirstChildOfClass("Humanoid")

        if humanoid then
            graph:Push(humanoid.Health)
        end
    end
end)
```
<img width="400" height="237" alt="image" src="https://github.com/user-attachments/assets/4ecb2494-49dc-4392-a4f9-cb1cd614a3c0" />

# Custom Themes

```lua
local Example = {
    -- Backgrounds
    WindowBg      = Color3.fromRGB(17, 14, 20),
    TitleBg       = Color3.fromRGB(22, 18, 27),
    Border        = Color3.fromRGB(56, 42, 66),

    -- Text
    Text          = Color3.fromRGB(245, 242, 248),
    SubText       = Color3.fromRGB(168, 160, 178),

    -- Accent
    Accent        = Color3.fromRGB(255, 92, 176),
    AccentHover   = Color3.fromRGB(255, 122, 194),

    -- Frames
    FrameBg       = Color3.fromRGB(24, 20, 30),
    FrameBgHover  = Color3.fromRGB(31, 26, 38),

    -- Toggles
    CheckOff      = Color3.fromRGB(22, 18, 27),
    CheckOn       = Color3.fromRGB(255, 92, 176),

    -- Sliders
    SliderTrack   = Color3.fromRGB(45, 38, 54),
    SliderFill    = Color3.fromRGB(255, 92, 176),

    -- Tabs
    TabBarBg      = Color3.fromRGB(22, 18, 27),
    TabNormal     = Color3.fromRGB(22, 18, 27),
    TabNormalText = Color3.fromRGB(168, 160, 178),

    TabActive     = Color3.fromRGB(33, 27, 41),
    TabActiveText = Color3.fromRGB(255, 92, 176),

    TabOff        = Color3.fromRGB(22, 18, 27),
    TabOn         = Color3.fromRGB(33, 27, 41),

    -- Graph
    GraphBg       = Color3.fromRGB(20, 17, 24),
    GraphLine     = Color3.fromRGB(255, 116, 189),
}
```

> To use this theme, you NEED to set it in the window just like this

```lua
local win = RGui.new("Rgui Demo", Example)--you need the comma, then you set the exact name of your theme.
```

<img width="406" height="304" alt="image" src="https://github.com/user-attachments/assets/d1249da4-8462-48fb-a7b9-26ce6361e40e" />

# WaterMarks 🚧WARNING this is a Beta Feature may have errors + not work as expected

> Static Example

```lua
local wm = win:CreateWatermark("Example Script", {
    TextColor = Color3.fromRGB(255, 255, 255),
    TextSize = 14,
    Position = UDim2.new(0, 2, 0, 2)
})
```

> Dynamic Example

```lua
local wm = win:CreateWatermark("Example Script", {
    TextColor = Color3.fromRGB(255, 255, 255),
    TextSize = 14,
    Position = UDim2.new(0, 2, 0, 2)
})

local version = 1

task.spawn(function()
    while task.wait(2) do
        version += 1

        wm:Update(string.format(
            "<font color='#FFFFFF'>Example Script <b>v1.%d</b></font>",
            version
        ))
    end
end)
```

<img width="473" height="35" alt="image" src="https://github.com/user-attachments/assets/c79fa482-4802-4900-aa73-d63d67f9d1f2" />
