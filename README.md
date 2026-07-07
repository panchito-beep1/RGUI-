[ThemeGenerator.html](https://github.com/user-attachments/files/29726419/ThemeGenerator.html)# RGUI The Imgui For Roblox
<img width="359" height="222" alt="image" src="https://github.com/user-attachments/assets/59ded38d-19d9-4bed-b09f-45a1b47594b2" />
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

# Graphs

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
> Also, if you want to create your own themes easily, you can use this theme generator
[Upl<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Luau Theme Generator</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&family=Fira+Code:wght@400;500&display=swap" rel="stylesheet">
    <style>
        :root {
            /* Generator App Colors */
            --bg-base: #09070d;
            --panel-bg: rgba(22, 18, 30, 0.45);
            --panel-border: rgba(167, 139, 250, 0.15);
            --accent: #a78bfa;
            --accent-hover: #c4b5fd;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --glow: rgba(167, 139, 250, 0.2);
        }

        * { box-sizing: border-box; }
        
        body { 
            margin: 0; padding: 3rem 2rem; 
            background: radial-gradient(circle at 50% -20%, #1a1525, var(--bg-base)); 
            background-attachment: fixed;
            color: var(--text-main); font-family: 'Inter', system-ui, sans-serif; 
            display: flex; justify-content: center; min-height: 100vh;
        }

        .container { 
            max-width: 1200px; width: 100%; 
            display: grid; grid-template-columns: 1fr 1.2fr; gap: 2.5rem; align-items: start;
        }
        @media (max-width: 850px) { .container { grid-template-columns: 1fr; } }

        .card { 
            background: var(--panel-bg); backdrop-filter: blur(16px); -webkit-backdrop-filter: blur(16px);
            padding: 2rem; border-radius: 16px; border: 1px solid var(--panel-border); 
            box-shadow: 0 20px 40px rgba(0,0,0,0.4), inset 0 1px 0 rgba(255,255,255,0.05); 
        }

        /* App Tabs */
        .tabs { 
            display: flex; background: rgba(0,0,0,0.2); border-radius: 10px;
            padding: 0.35rem; margin-bottom: 1.5rem; border: 1px solid var(--panel-border);
        }
        .tab { 
            flex: 1; text-align: center; padding: 0.75rem 1rem; cursor: pointer; 
            color: var(--text-muted); font-weight: 500; font-size: 0.9rem;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1); border-radius: 8px;
        }
        .tab:hover { color: var(--text-main); }
        .tab.active { background: var(--accent); color: #09070d; font-weight: 600; box-shadow: 0 4px 12px var(--glow); }

        /* Inputs */
        .input-group { 
            display: flex; justify-content: space-between; align-items: center; 
            padding: 0.6rem 0; border-bottom: 1px solid rgba(255,255,255,0.03); transition: background 0.2s;
        }
        .input-group:hover { background: rgba(255,255,255,0.02); border-radius: 6px; padding: 0.6rem 0.5rem; margin: 0 -0.5rem; }
        .input-group:last-child { border-bottom: none; }
        .input-label { font-size: 0.9rem; color: var(--text-main); font-weight: 500;}
        .section-label { margin-top: 1.5rem; margin-bottom: 0.75rem; font-size: 0.7rem; text-transform: uppercase; letter-spacing: 1.5px; color: var(--accent); font-weight: 600; }

        input[type="text"] {
            background: rgba(0,0,0,0.3); border: 1px solid var(--panel-border);
            color: var(--text-main); padding: 0.5rem 0.75rem; border-radius: 6px;
            font-family: 'Fira Code', monospace; font-size: 0.85rem; width: 160px; outline: none;
            text-align: right;
        }
        input[type="text"]:focus { border-color: var(--accent); }

        input[type="color"] { -webkit-appearance: none; border: none; width: 32px; height: 32px; border-radius: 50%; cursor: pointer; background: none; padding: 0; outline: none; }
        input[type="color"]::-webkit-color-swatch-wrapper { padding: 0; }
        input[type="color"]::-webkit-color-swatch { border: 2px solid rgba(255,255,255,0.1); border-radius: 50%; transition: transform 0.2s; }
        input[type="color"]:hover::-webkit-color-swatch { transform: scale(1.1); border-color: var(--accent); }

        /* Code Block */
        .code-preview { 
            background: rgba(0, 0, 0, 0.4); padding: 1.5rem; border-radius: 12px; 
            font-family: 'Fira Code', monospace; font-size: 0.85rem; color: #e2e8f0; 
            overflow-x: auto; white-space: pre; line-height: 1.6; margin-bottom: 1.5rem; 
            border: 1px solid rgba(0,0,0,0.5); box-shadow: inset 0 4px 10px rgba(0,0,0,0.2);
            height: 480px; 
        }
        .code-preview::-webkit-scrollbar { height: 8px; width: 8px;}
        .code-preview::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.1); border-radius: 4px; }
        
        .keyword { color: #c678dd; } .function { color: #61afef; } 
        .comment { color: #5c6370; font-style: italic; } .number { color: #d19a66; } .property { color: #e06c75; }

        button { width: 100%; background: var(--accent); color: #09070d; border: none; padding: 1rem; border-radius: 10px; font-weight: 600; font-size: 1rem; cursor: pointer; transition: all 0.2s; font-family: 'Inter', sans-serif; }
        button:hover { background: var(--accent-hover); transform: translateY(-2px); box-shadow: 0 8px 20px var(--glow); }

        /* --- EXACT REPLICA UI PREVIEW STYLES --- */
        #visual-preview-container {
            height: 480px;
            margin-bottom: 1.5rem;
            display: flex;
            align-items: center;
            justify-content: center;
            background: repeating-linear-gradient(
                45deg,
                rgba(255, 255, 255, 0.02),
                rgba(255, 255, 255, 0.02) 10px,
                rgba(0, 0, 0, 0.02) 10px,
                rgba(0, 0, 0, 0.02) 20px
            ), rgba(0,0,0,0.3);
            border-radius: 12px;
            border: 1px dashed rgba(255,255,255,0.1);
            position: relative;
            overflow: hidden;
        }

        /* Floating FPS Box */
        .mock-fps-box {
            position: absolute;
            top: 20px;
            left: 20px;
            background: var(--p-WindowBg);
            border: 1px solid var(--p-Border);
            color: var(--p-Text);
            padding: 6px 10px;
            font-family: 'Fira Code', monospace;
            font-size: 11px;
            border-radius: 2px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.3);
        }

        /* Main Window */
        .mock-window {
            width: 420px;
            background: var(--p-WindowBg);
            border: 1px solid var(--p-Border);
            border-radius: 2px;
            font-family: 'Fira Code', monospace; /* Monospace for the exact script hub look */
            color: var(--p-Text);
            box-shadow: 0 15px 35px rgba(0,0,0,0.6);
            display: flex;
            flex-direction: column;
        }
        
        .mock-titlebar { 
            background: var(--p-TitleBg); 
            padding: 8px 12px; 
            font-size: 12px; 
            display: flex; 
            justify-content: space-between; 
            border-bottom: 1px solid var(--p-Border); 
        }
        
        .mock-tabs { 
            display: flex; 
            background: var(--p-TabBarBg); 
            border-bottom: 1px solid var(--p-Border); 
        }
        .mock-tab { 
            padding: 8px 14px; 
            font-size: 11px; 
            border-right: 1px solid var(--p-Border); 
        }
        .mock-tab.active { background: var(--p-TabOn); color: var(--p-TabActiveText); }
        .mock-tab.inactive { background: var(--p-TabOff); color: var(--p-TabNormalText); }
        .mock-tab-filler { flex-grow: 1; background: var(--p-TabBarBg); } /* Empty space on right of tabs */
        
        .mock-content { padding: 12px; background: var(--p-WindowBg); }
        
        .mock-section-title { 
            color: var(--p-SubText); 
            font-size: 11px; 
            margin-bottom: 10px; 
            margin-top: 4px;
        }
        
        /* The blocky rows for elements */
        .mock-row { 
            background: var(--p-FrameBg); 
            border: 1px solid var(--p-Border); 
            border-radius: 2px; 
            margin-bottom: 6px; 
            padding: 6px 10px; 
            display: flex; 
            align-items: center; 
            gap: 10px; 
            font-size: 11px;
            min-height: 28px;
            position: relative;
        }

        /* Checkboxes */
        .mock-checkbox { 
            width: 14px; 
            height: 14px; 
            border: 1px solid var(--p-Border); 
            background: var(--p-CheckOff); 
            border-radius: 2px;
            padding: 1px;
        }
        .mock-checkbox.checked .mock-checkbox-fill {
            width: 100%;
            height: 100%;
            background: var(--p-CheckOn);
            border-radius: 1px;
        }

        /* Sliders */
        .mock-row.is-slider { padding: 0; overflow: hidden; justify-content: flex-start; }
        .mock-slider-bg { 
            background: var(--p-SliderTrack); 
            width: 100%; 
            height: 100%; 
            position: absolute; 
            top: 0; left: 0; 
            z-index: 1;
        }
        .mock-slider-fill { 
            background: var(--p-SliderFill); 
            height: 100%; 
            position: absolute; 
            top: 0; left: 0; 
            z-index: 2;
        }
        .mock-slider-text {
            position: relative;
            z-index: 3;
            width: 100%;
            text-align: center;
            padding: 6px 0;
            color: var(--p-Text);
            text-shadow: 1px 1px 1px rgba(0,0,0,0.5); /* Helps text pop over light fills */
        }

        /* Color Picker */
        .mock-row.is-color-picker { justify-content: space-between; }
        .mock-color-swatch {
            width: 14px;
            height: 14px;
            background: #ff66cc; /* Hardcoded pink to match the screenshot */
            border-radius: 2px;
        }

        .helper-text { font-size: 0.85rem; color: var(--text-muted); margin-bottom: 1.5rem; line-height: 1.5; }
    </style>
</head>
<body>

<div class="container">
    <div class="card" style="max-height: 90vh; overflow-y: auto;">
        
        <div class="input-group" style="margin-bottom: 1.5rem; background: rgba(0,0,0,0.2); padding: 10px; border-radius: 8px; border: 1px solid var(--panel-border);">
            <span class="input-label" style="color: var(--accent);">Theme Name</span>
            <input type="text" id="theme-name" value="Zenith Premium" oninput="updateGlobals()">
        </div>

        <div class="tabs">
            <div class="tab active" onclick="switchInputMode('simple')" id="tab-in-simple">Simple Mode</div>
            <div class="tab" onclick="switchInputMode('full')" id="tab-in-full">Full Mode</div>
        </div>

        <div id="mode-simple">
            <p class="helper-text">Select your base colors. The engine will calculate all variations for the UI preview.</p>
            <div class="input-group">
                <span class="input-label">Background Base</span>
                <input type="color" id="base-bg" value="#0c0c0e" oninput="generateFromSimple()">
            </div>
            <div class="input-group">
                <span class="input-label">Text Color</span>
                <input type="color" id="base-text" value="#f5f5f5" oninput="generateFromSimple()">
            </div>
            <div class="input-group">
                <span class="input-label">Accent Highlight</span>
                <input type="color" id="base-accent" value="#a78bfa" oninput="generateFromSimple()">
            </div>
        </div>

        <div id="mode-full" style="display: none;">
            <p class="helper-text">Fine-tune specific elements to see them update live in the preview.</p>
            <div id="full-inputs-container"></div>
        </div>
    </div>

    <div class="card">
        <div class="tabs" style="margin-bottom: 1rem;">
            <div class="tab active" onclick="switchOutputMode('visual')" id="tab-out-visual">UI Preview</div>
            <div class="tab" onclick="switchOutputMode('code')" id="tab-out-code">Luau Code</div>
        </div>

        <div id="visual-preview-container">
            <div class="mock-fps-box">FPS: 136 &nbsp;Ping: 165 ms</div>
            
            <div class="mock-window" id="mock-ui">
                <div class="mock-titlebar">
                    <span id="preview-title-display">Zenith Premium</span>
                    <span style="opacity: 0.7;">- &nbsp; x</span>
                </div>
                
                <div class="mock-tabs">
                    <div class="mock-tab inactive">Aimbot</div>
                    <div class="mock-tab inactive">Triggerbot</div>
                    <div class="mock-tab active">Visuals</div>
                    <div class="mock-tab inactive">ESP</div>
                    <div class="mock-tab inactive">Settings</div>
                    <div class="mock-tab-filler"></div>
                </div>

                <div class="mock-content">
                    <div class="mock-section-title">--- FOV Circle ---</div>
                    
                    <div class="mock-row">
                        <div class="mock-checkbox checked"><div class="mock-checkbox-fill"></div></div>
                        <span>Show FOV</span>
                    </div>
                    
                    <div class="mock-row">
                        <div class="mock-checkbox"></div>
                        <span>Filled FOV</span>
                    </div>
                    
                    <div class="mock-row is-slider">
                        <div class="mock-slider-bg"></div>
                        <div class="mock-slider-fill" style="width: 65%;"></div>
                        <div class="mock-slider-text"></div> </div>

                    <div class="mock-row is-slider">
                        <div class="mock-slider-bg"></div>
                        <div class="mock-slider-fill" style="width: 25%;"></div>
                        <div class="mock-slider-text">FOV Thickness: 2</div>
                    </div>
                    
                    <div class="mock-row">
                        <div class="mock-checkbox"></div>
                        <span>Rainbow FOV</span>
                    </div>

                    <div class="mock-row is-color-picker">
                        <span>FOV Color</span>
                        <div class="mock-color-swatch"></div>
                    </div>

                    <div class="mock-section-title" style="margin-top: 14px;">--- Crosshair ---</div>
                    
                    <div class="mock-row" style="margin-bottom: 0; border-bottom-left-radius: 0; border-bottom-right-radius: 0; border-bottom: none;">
                        <div class="mock-checkbox"></div>
                        <span>Show Crosshair</span>
                    </div>
                </div>
            </div>
        </div>

        <div class="code-preview" id="code-output" style="display: none;"></div>
        
        <button onclick="copyCode()" id="copy-btn">Copy Luau Code</button>
    </div>
</div>

<script>
    const themeStructure = {
        "Main": { WindowBg: "#0c0c0e", TitleBg: "#0c0c0e", Border: "#37373c" },
        "Text": { Text: "#f5f5f5", SubText: "#aaaaaf" },
        "Accent": { Accent: "#a78bfa", AccentHover: "#c4b5fd" },
        "Frames": { FrameBg: "#121215", FrameBgHover: "#19191d" },
        "Checkbox": { CheckOff: "#0e0e10", CheckOn: "#b4b4b4" },
        "Slider": { SliderTrack: "#1f1f23", SliderFill: "#b4b4b4" },
        "Tabs": { 
            TabBarBg: "#0c0c0e", TabNormal: "#0c0c0e", TabNormalText: "#a5a5aa", 
            TabActive: "#121215", TabActiveText: "#f5f5f5", TabOff: "#0c0c0e", TabOn: "#121215" 
        },
        "Graph": { GraphBg: "#0e0e10", GraphLine: "#b4b4b4" },
        "Notifications": { NotifyBg: "#121215", NotifyTitle: "#f5f5f5", NotifyMsg: "#bebec3" }
    };

    let flatTheme = {};

    function init() {
        const container = document.getElementById('full-inputs-container');
        for (const [category, keys] of Object.entries(themeStructure)) {
            const section = document.createElement('div');
            section.className = 'section-label'; section.innerText = category;
            container.appendChild(section);

            for (const [key, defaultHex] of Object.entries(keys)) {
                flatTheme[key] = defaultHex; 
                const group = document.createElement('div');
                group.className = 'input-group';
                group.innerHTML = `
                    <span class="input-label">${key}</span>
                    <input type="color" id="input-${key}" value="${defaultHex}" oninput="updateColor('${key}', this.value)">
                `;
                container.appendChild(group);
            }
        }
        updateGlobals();
    }

    function switchInputMode(mode) {
        document.getElementById('tab-in-simple').classList.toggle('active', mode === 'simple');
        document.getElementById('tab-in-full').classList.toggle('active', mode === 'full');
        document.getElementById('mode-simple').style.display = mode === 'simple' ? 'block' : 'none';
        document.getElementById('mode-full').style.display = mode === 'full' ? 'block' : 'none';
        if (mode === 'simple') generateFromSimple();
    }

    function switchOutputMode(mode) {
        document.getElementById('tab-out-visual').classList.toggle('active', mode === 'visual');
        document.getElementById('tab-out-code').classList.toggle('active', mode === 'code');
        document.getElementById('visual-preview-container').style.display = mode === 'visual' ? 'flex' : 'none';
        document.getElementById('code-output').style.display = mode === 'code' ? 'block' : 'none';
    }

    function offsetColor(hex, offset) {
        let r = parseInt(hex.slice(1, 3), 16); let g = parseInt(hex.slice(3, 5), 16); let b = parseInt(hex.slice(5, 7), 16);
        r = Math.max(0, Math.min(255, r + offset)); g = Math.max(0, Math.min(255, g + offset)); b = Math.max(0, Math.min(255, b + offset));
        return "#" + (1 << 24 | r << 16 | g << 8 | b).toString(16).slice(1).padStart(6, '0');
    }

    function hexToLuauRGB(hex) {
        let r = parseInt(hex.slice(1, 3), 16); let g = parseInt(hex.slice(3, 5), 16); let b = parseInt(hex.slice(5, 7), 16);
        return `<span class="function">Color3.fromRGB</span>(<span class="number">${r}</span>, <span class="number">${g}</span>, <span class="number">${b}</span>)`;
    }

    function updateGlobals() {
        const titleInput = document.getElementById('theme-name').value;
        document.getElementById('preview-title-display').innerText = titleInput || "Custom Theme";
        updateCodePreview();
        updateVisualPreview();
    }

    function generateFromSimple() {
        const bg = document.getElementById('base-bg').value;
        const txt = document.getElementById('base-text').value;
        const acc = document.getElementById('base-accent').value;

        // Tweaked logic to match the flatter, blocky look of the screenshot
        const newTheme = {
            WindowBg: bg, TitleBg: bg, Border: offsetColor(bg, 40),
            Text: txt, SubText: offsetColor(txt, -75),
            Accent: acc, AccentHover: offsetColor(acc, 30),
            FrameBg: offsetColor(bg, 5), FrameBgHover: offsetColor(bg, 10),
            CheckOff: bg, CheckOn: acc,
            SliderTrack: offsetColor(bg, 15), SliderFill: acc,
            TabBarBg: bg, TabNormal: bg, TabNormalText: offsetColor(txt, -80),
            TabActive: offsetColor(bg, 5), TabActiveText: txt, TabOff: bg, TabOn: offsetColor(bg, 5),
            GraphBg: bg, GraphLine: acc,
            NotifyBg: offsetColor(bg, 5), NotifyTitle: txt, NotifyMsg: offsetColor(txt, -55)
        };

        for (const [key, hex] of Object.entries(newTheme)) {
            flatTheme[key] = hex;
            const inputElement = document.getElementById(`input-${key}`);
            if (inputElement) inputElement.value = hex;
        }
        updateGlobals();
    }

    function updateColor(key, hex) {
        flatTheme[key] = hex;
        updateCodePreview();
        updateVisualPreview();
    }

    function updateVisualPreview() {
        const ui = document.getElementById('mock-ui');
        const fps = document.querySelector('.mock-fps-box');
        
        // Apply CSS Variables so the HTML dynamically changes
        for (const [key, hex] of Object.entries(flatTheme)) {
            ui.style.setProperty(`--p-${key}`, hex);
            fps.style.setProperty(`--p-${key}`, hex);
        }
    }

    function updateCodePreview() {
        // Strip spaces from the Theme Name to make a valid Luau variable name
        let rawName = document.getElementById('theme-name').value;
        let luaTableName = rawName.replace(/[^a-zA-Z0-9_]/g, '');
        if (!luaTableName) luaTableName = "CustomTheme"; // Fallback

        let luaStr = `<span class="keyword">local</span> ${luaTableName} = {\n`;
        for (const [category, keys] of Object.entries(themeStructure)) {
            luaStr += `    <span class="comment">-- ${category}</span>\n`;
            for (const key of Object.keys(keys)) {
                const spacing = " ".repeat(14 - key.length); 
                luaStr += `    <span class="property">${key}</span>${spacing}= ${hexToLuauRGB(flatTheme[key])},\n`;
            }
            luaStr += `\n`;
        }
        luaStr = luaStr.slice(0, -2) + `\n}`;
        document.getElementById('code-output').innerHTML = luaStr;
    }

    function copyCode() {
        const rawCode = document.getElementById('code-output').innerText;
        navigator.clipboard.writeText(rawCode).then(() => {
            const btn = document.getElementById('copy-btn');
            btn.innerText = "✓ Copied to Clipboard!";
            btn.style.background = "#34d399"; btn.style.color = "#000";
            setTimeout(() => { btn.innerText = "Copy Luau Code"; btn.style.background = "var(--accent)"; }, 2500);
        });
    }

    window.onload = init;
</script>

</body>
</html>oading ThemeGenerator.html…]()

<img width="406" height="304" alt="image" src="https://github.com/user-attachments/assets/d1249da4-8462-48fb-a7b9-26ce6361e40e" />

# WaterMarks
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


# Me

<a href="https://rscripts.net/user/GoatedCitizen" target="_blank"><img alt="GoatedCitizen on Rscripts" loading="lazy" width="360" height="132" src="https://rscripts.net/api/embed/user/GoatedCitizen?theme=dark" /></a>
