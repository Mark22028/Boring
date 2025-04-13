-- Load the library (assuming it's in the same directory)
```local ZIvyer = loadstring(game:HttpGet("https://raw.githubusercontent.com/Mark22028/Boring/refs/heads/main/ZIvyerUILib.txt"))()```

---------------------------------------------------------------------------------
-- Basic Setup
---------------------------------------------------------------------------------

# Create a new UI with customized intro (intro will always show for 5 seconds)
```
local UI = ZIvyer.new({
    UIName = "My Super Smooth App", -- Name of the UI in Explorer
    IntroTitle = "My Super App", -- Title shown in intro
    IntroDescription = "Experience the super duper ultra ultimate smoothness" -- Description in intro
})
```
## All themes are available: Dark, Light, Black, Green, Cyan, Blue, Diamond, Gold, Yellow, Pink, Gray/Grey, Red, Orange, Purple, Violet, White
```UI:SetTheme("Dark") -- Start with Dark theme```

---------------------------------------------------------------------------------
-- Windows
---------------------------------------------------------------------------------

# Create a main window
```local mainWindow = UI:CreateWindow("Main Features", UDim2.new(0, 400, 0, 350))```
# Create a settings window
```local settingsWindow = UI:CreateWindow("Settings", UDim2.new(0, 350, 0, 300), UDim2.new(0.7, 0, 0.3, 0))```
# Create a premium window (only visible when premium is enabled)
```local premiumWindow = UI:CreateWindow("Premium Features", UDim2.new(0, 350, 0, 300), UDim2.new(0.3, 0, 0.7, 0), true)```

---------------------------------------------------------------------------------
-- Elements - Main Window
---------------------------------------------------------------------------------

# Section helps organize elements
```local generalSection = mainWindow:AddSection("General Controls")```
# Add a label (static text)
```generalSection:AddLabel("Texts or Version")```
# Add a paragraph for more detailed information
```generalSection:AddParagraph("About", "ZIvyer UI Library provides super duper ultra ultimate smooth animations and modern UI elements for your Roblox games.")```
# Add a button with callback function
```
mainWindow:AddButton("Click Me", function()
    print("Button clicked!")
    -- You could animate the button by adding particle bursts here
    -- But notifications are disabled in the library by request
end)
```
# Add a toggle switch
```
local myToggle = mainWindow:AddToggle("Enable Feature", function(state)
    print("Toggle state:", state)
    -- This would enable/disable some feature in your game
end)
```
# Add a slider
```
local mySlider = mainWindow:AddSlider("Intensity", 0, 100, 50, function(value)
    print("Slider value:", value)
    -- You would use this value to control something in your game
end)
```
# Add a textbox
```
local myTextBox = mainWindow:AddTextBox("Username", "Enter text here...", function(text)
    print("Text entered:", text)
    -- You would use this to get user input
end)
```
# Add a dropdown menu
```
local options = {"Option 1", "Option 2", "Option 3"}
local myDropdown = mainWindow:AddDropdown("Select Option", options, function(selected)
    print("Selected option:", selected)
    -- You would handle the selected option here
end)
```
# Add a colorpicker
```
local myColorPicker = mainWindow:AddColorPicker("Choose Color", Color3.new(1, 0, 0), function(color)
    print("Color selected:", color)
    -- You would use this color in your game
end)
```

---------------------------------------------------------------------------------
-- Elements - Settings Window
---------------------------------------------------------------------------------

# Theme Section
```
local themeSection = settingsWindow:AddSection("Theme Settings")
themeSection:EnableRainbowOutline(true) -- Add fancy rainbow outline to this section
```
# Add theme selector buttons
```
local themeOptions = {"Dark", "Light", "Black", "Green", "Cyan", "Blue", "Diamond", 
                      "Gold", "Yellow", "Pink", "Gray", "Red", "Orange", "Purple", "Violet", "White"}

for _, theme in ipairs(themeOptions) do
    settingsWindow:AddButton("Theme: " .. theme, function()
        UI:SetTheme(theme)
    end)
end
```
# Add custom theme creator
```
settingsWindow:AddTextBox("Custom RGB", "255,0,0", function(text)
    -- Create a custom theme from RGB values
    UI:CreateThemeFromRobloxId("CustomTheme", text, false)
    UI:SetTheme("CustomTheme")
end)

settingsWindow:AddTextBox("Roblox Image ID", "12345678", function(text)
    -- Create a theme with a custom background image
    UI:CreateThemeFromRobloxId("ImageTheme", text, true)
    UI:SetTheme("ImageTheme")
end)
```
# UI Settings
```local uiSection = settingsWindow:AddSection("UI Settings")```
# Add toggle for UI visibility
```
uiSection:AddButton("Toggle UI", function()
    UI:ToggleUI()
end)
```
# Add button to destroy UI 
```
uiSection:AddButton("Destroy UI", function()
    UI:Destroy()
end)
```

---------------------------------------------------------------------------------
-- Premium Features
---------------------------------------------------------------------------------

# Set up key system (keys that will allow premium access)
```UI:SetupKeySystem({"PREMIUM123", "ZIVYER2023"}, 3) -- valid keys, max attempts```
# Add button to open key verification window
```
settingsWindow:AddButton("Enter Premium Key", function()
    UI:ShowKeyWindow("ZIvyer Premium", "Enter your premium key below to unlock exclusive features", 
        function() 
            -- Success callback
            print("Key verification successful!")
        end,
        function(attempts, maxAttempts) 
            -- Failure callback
            print("Invalid key! Attempts: " .. attempts .. "/" .. maxAttempts)
        end,
        function() 
            -- Too many attempts callback
            print("Too many failed attempts. Try again later.")
        end,
        true -- Enable premium features on success, false if no
    )
end)
```
# Directly enable premium without key (for testing)
```
local devSection = settingsWindow:AddSection("Developer Options")
devSection:AddToggle("Enable Premium", function(state)
    UI:SetPremiumOnlyEnabled(state)
end)
```
# Add premium-only elements
```
local premiumSection = premiumWindow:AddSection("Exclusive Features")
premiumSection:EnableRainbowOutline(true) -- Rainbow glow for premium
```
# Special premium-only buttons with extra particle effects
```
premiumWindow:AddButton("Premium Particle Burst", function()
    -- This would create special effects in your game
    print("Premium feature activated!")
end, true) -- The 'true' parameter marks this as premium-only
```
# Premium-only slider with enhanced visuals
```
premiumWindow:AddSlider("Premium Power", 0, 1000, 500, function(value)
    print("Premium power set to:", value)
end, true) -- Premium-only
```
# Enable premium feature toggle (would be false until premium is activated)
```print("Premium status:", UI:IsPremiumOnly())```




---------------------------------------------------------------------------------
-- Full PremiumOnly Examples
---------------------------------------------------------------------------------

# PREMIUM WINDOWS EXAMPLE
-- ---------------------
```
-- Create a premium-only window (the true at the end makes it premium-only)
local premiumWindow = UI:CreateWindow("Premium Window", UDim2.new(0, 450, 0, 350), UDim2.new(0.5, 0, 0.5, 0), true)

-- Create a regular window for comparison
local regularWindow = UI:CreateWindow("Regular Window", UDim2.new(0, 400, 0, 300), UDim2.new(0.2, 0, 0.2, 0))
```
# PREMIUM SECTIONS EXAMPLE
-- ----------------------
```
-- Add a premium section (the true at the end makes it premium-only)
local premiumSection = regularWindow:AddSection("Premium Section", true)

-- Add a regular section for comparison
local regularSection = regularWindow:AddSection("Regular Section")
```
# PREMIUM TABS EXAMPLE
-- ------------------
```
-- Add a premium tab (the true at the end makes it premium-only)
local premiumTab = regularWindow:AddTab("Premium Tab", true)

-- Add a regular tab for comparison
local regularTab = regularWindow:AddTab("Regular Tab")
```
# PREMIUM ELEMENTS EXAMPLE
-- ----------------------
```
# BUTTONS
-- Premium button in regular section (notice the true at the end)
regularSection:AddButton("Premium Button", function()
    print("Premium button clicked")
end, true)

-- Regular button for comparison
regularSection:AddButton("Regular Button", function()
    print("Regular button clicked")
end)

# TOGGLES
-- Premium toggle (notice the true at the end)
regularSection:AddToggle("Premium Toggle", function(enabled)
    print("Premium toggle:", enabled)
end, true)

-- Regular toggle for comparison
regularSection:AddToggle("Regular Toggle", function(enabled)
    print("Regular toggle:", enabled)
end)

# SLIDERS
-- Premium slider (notice the true at the end)
regularSection:AddSlider("Premium Slider", 0, 100, 50, function(value)
    print("Premium slider value:", value)
end, true)

-- Regular slider for comparison
regularSection:AddSlider("Regular Slider", 0, 100, 50, function(value)
    print("Regular slider value:", value)
end)

# DROPDOWNS
-- Premium dropdown (notice the true at the end)
regularSection:AddDropdown("Premium Dropdown", {"Option 1", "Option 2", "Option 3"}, function(selected)
    print("Premium dropdown selected:", selected)
end, true)

-- Regular dropdown for comparison
regularSection:AddDropdown("Regular Dropdown", {"Option 1", "Option 2", "Option 3"}, function(selected)
    print("Regular dropdown selected:", selected)
end)

# TEXTBOXES
-- Premium textbox (notice the true at the end)
regularSection:AddTextBox("Premium TextBox", "Enter premium text...", function(text)
    print("Premium textbox text:", text)
end, true)

-- Regular textbox for comparison
regularSection:AddTextBox("Regular TextBox", "Enter text...", function(text)
    print("Regular textbox text:", text)
end)

# COLOR PICKERS
-- Premium color picker (notice the true at the end)
regularSection:AddColorPicker("Premium Color", Color3.fromRGB(255, 0, 0), function(color)
    print("Premium color selected:", color)
end, true)

-- Regular color picker for comparison
regularSection:AddColorPicker("Regular Color", Color3.fromRGB(0, 255, 0), function(color)
    print("Regular color selected:", color)
end)

# PARAGRAPHS
-- Premium paragraph (notice the true at the end)
regularSection:AddParagraph("Premium Info", "This is premium content with ultra-smooth animations", nil, nil, true)

-- Regular paragraph for comparison
regularSection:AddParagraph("Regular Info", "This is regular content with ultra-smooth animations")

# LABELS
-- Premium label (notice the true at the end)
regularSection:AddLabel("Premium Label Text", true)

-- Regular label for comparison
regularSection:AddLabel("Regular Label Text")

# PREMIUM TAB ELEMENTS
-- ------------------
-- You can add premium elements to premium tabs too
premiumTab:AddButton("Tab Premium Button", function()
    print("Tab premium button clicked")
end)

-- Or regular elements to premium tabs (they're premium by association)
premiumTab:AddToggle("Tab Toggle", function(enabled)
    print("Tab toggle:", enabled)
end)

-- You can add premium elements to regular tabs too
regularTab:AddButton("Premium in Regular Tab", function()
    print("Premium button in regular tab clicked")
end, true)

# PREMIUM SECTION ELEMENTS
-- ----------------------
-- You can add premium elements to premium sections too (already premium by association)
premiumSection:AddButton("Section Premium Button", function()
    print("Section premium button clicked")
end)

-- Special premium section
premiumSection:EnableRainbowOutline(true) -- Add rainbow animation to the outline
```
# CONTROLLING PREMIUM ACCESS
-- ------------------------
-- Enable all premium elements
```UI:SetPremiumOnlyEnabled(true)```

-- To disable premium elements, you would use:
-- UI:SetPremiumOnlyEnabled(false)
