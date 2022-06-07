# Vision Lib Documentation

## The Library
```lua
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Vision-Software-LLC/Vision-UI/main/source"))()
```

## Creating a Window
```lua
local window = Library:CreateWindow({
	PrimaryColor = Color3.fromRGB(35, 35, 35), -- Defualt is 35, 35, 35
	SecondaryColor = Color3.fromRGB(40, 40, 40), -- Defualt is 40, 40, 40
	FooterColor = Color3.fromRGB(45, 45, 45), -- Defualt is 45, 45, 45
	Title = "Vision UI", -- Defualt is "Vision UI"
	TitleSize = 16, -- Defualt is 16
	
	ToggleBind = "RightShift", -- Enum.KeyCode.RightShift (Just put in key of keycode)
	SkipStartup = false,
	Footer = true
})

--[[

PrimaryColor = The default primarycolor (UI Background)
SecondaryColor = The default secondarycolor (Button Backgrounds)
FooterColor = The default color of the footer.
Title = The title of your ui
TitleSize = The fontsize of the title
ToggleBind = Bind for toggling visibiltity of the gui
SkipStartup = Skip the startup animation. Sound still plays.
Footer = Toggle on or off the footer.

]]
```

## Creating a Tab
```lua
local tab = window:CreateTab({
  Text = "Tab",
  Icon = "rbxassetid://7104816810",
  CanvasSize = 2,
  Default = true
})

--[[

Text = Name of the tab, text in tab button.
Icon = The icon on the tab. Shows up next to the tab button.
CanvasSize = The size of the scrolling box, you can set this to however tall you require. I have not implemented dynamic CanvasSize for tabs but I have for Dropdown.
Default = If this is the default tab, set this to true.

]]
```

## Creating a Button
```lua
tab:CreateButton({
  Text = "Button",
  Callback = function()
    -- Script here
  end
})

--[[

Text = The button text
Callback = The script/function executed after the button is pressed

]]
```

## Creating a Toggle
```lua
tab:CreateToggle({
  Text = "Toggle",
  Default = true,
  Callback = function(state)
    print("Toggle: "..tostring(state))
  end
})

--[[

Text = The toggle text
Default = The default state of the toggle
Callback = The script/function executed after the toggle is pressed

]]
```


## Creating a Slider
```lua
tab:CreateSlider({
  Text = "Slider",
  ValueOnly = "bananas",
  Scale = 1,
  Default = 50,
  Callback = function(value)
    print("Slider Value: " .. value)
  end
})

--[[

Text = The slider text
ValueOnly = Text that appears after shown value. E.g. 50 bananas, or slider is moved, 20 bananas.
Scale = The range of the slider. 0.1 = 0-10, 1 = 0-100, 2 = 0-100, etc...
Callback = The script/function executed after the slider value is changed

]]
```

## Creating a Dropdown
```lua
tab:CreateDropdown({
  Text = "Dropdown",
  MultiSelect = false,
  Selections = {"Option 1", "Option 2", "Option 3"},
  Default = 1, -- Index of default selection
  Callback = function(option)
    print("Dropdown: "..option)
  end
})

--[[

Text = The dropdown text
MultiSelect = Give the user the ability to select multiple items in the dropdown. Returns a table of selected values.

-- ONLY WITH MULTISELECT ENABLED : Default can be set to a table (eg. {1,2,5} ) of the default indexes of your selection.

Selection = The available options/selections for the user to choose from displayed in the dropdown.
Default = The default selection. Uses index values, 1 = option 1, 2 = option 2, etc... Set this to 0 for no default selection.
Callback = The script/function executed after the dropdown selection is changed

]]
```

## Creating a Colorpicker
```lua
tab:CreateColorPicker({
  Text = "Color Picker",
  Default = Color3.fromRGB(255, 255, 255), --// I think I broke this will fix later
  Callback = function(color)
    print("HSV: "..tostring(color)) -- For rgb just multiply by 255
  end
})

--[[

Text = The color picker text
Default = The colorpickers default color.
Callback = The script/function executed after the color value is changed

]]
```

## Creating tab spacing
```lua
window:CreateSpacing()

--// No args available. Support for the size argument will be added later
```

## Creating button spacing
```lua
Home:CreateSpacing({
  Size = 2,
})

--// Size = Spacing size; 1 = 1 buttons size of spacing, 2 = 2 buttons size of spacing, etc.
```

## Creating a keybind
```lua
tab:CreateKeybind({
  Text = "Keybind",
  Default = "F",
  Callback = function(held,keycode)
    print("Keydown: "..tostring(held))
    print("Keycode: "..tostring(keycode))
  end
})

--[[

Text = Keybind text/name
Default = Default key. Currently only a-z binds are accepted. Will be fixed later.
Callback = The function executed when the keybind is pressed down or let go of. Returns 2 arguments : held and keycode. Held is the status of the key and keycode is the keys keycode. Both returned each time the set key is pressed down or let go of.

]]
```

## Creating an input box
```lua
tab:CreateInput({
  Text = "Input",
  ValueOnly = true,
  Callback = function(input)
    print("Input: "..input)
  end
})

--[[

Text = Input box name/text
ValueOnly = True ~ Only accept values in the input box. False ~ Accept values and letters.
Callback = The function executed when focus is lost from the textbox (Enter is pressed or user clicks off).

]]
```

## Creating a tab button
```lua
local tabbutton = window:CreateTabButton({
  Text = "Tab Button",
  Icon = "rbxassetid://9766676906",
  Callback = function()
    -- script here
  end
})

--[[

Text = Tab Button text/name
Icon = Tab Button Icon
Callback = The function/script executed when you click this tab.

]]
```

## Destroying the UI
```lua
window:Destroy()
```

## Changing the Window Toggle button
```lua
window:ChangeToggleBind({
  NewBind = "RightShift"
})

--// NewBind = The new toggle window bind. The keyname from Enum.KeyCode.RightShift
```

## Window toggle alternative
```lua
window:Visible(true)

--// Only arg (true) is a bool based on whether or not the window should be visible. true to be visible, false for invisible.
:heheheha:
```

## Built in icons
```lua
local icons = Library:Icons()
--[[

The only current icons are as follows:
icons.FluentIcons
icons.FeatherIcons

Fluent and FeatherIcons are different styles. The tab icons we actually have are:

Home,
Aimbot,
Visuals,
Player,
Misc,
Settings,
Credits,
Exit

]]

-- Usage:

RandomImageLabel.Image = icons.FluentIcons.Settings
-- or
RandomImageLabel.Image = icons.FeatherIcons.Settings
```

## Built in Settings Tab
```lua
window:SettingsTab({
	Visible = true,
	Text = "Settings",
	Icon = icons.FluentIcons.Settings,
	EnabledSettings = {
		PrimaryColor = true,
		SecondaryColor = true,
		FooterColor = true,
		ButtonBorderColor = true,
		TextColor = true,
		CheckboxColor = true,
		SelectorColor = true,
		SliderPrimaryColor = true,
		SliderBackgroundColor = true
	}
})

--[[

Visible = The Setting Tabs Visibility. True by default
Text = Name/Text of the tab
Icon = Icon of the tab
EnabledSettings = The settings/color pickers that will be shown in the settings tab. Button to reset all colors to default will always be included.

]]
```

## Settings Colors
```lua
window:SetColor(object,color)

--[[

object = The object that you wish to change color. See below for all possible objects.
color = The color that you wish for the object to be.

]]

```
## Possible Objects for SetColor
```lua
PrimaryColor
SecondaryColor
FooterColor
ButtonBorderColor
TextColor
CheckboxColor
SelectorColor
SliderPrimaryColor
SliderBackgroundColor
```

## Creating a Notification
```lua
Library:Notification({
	Title = "Vision Lib Example",
	Text = "This is a notification",
	Icon = "rbxassetid://9838878267",
	Duration = 5,
	
	Theme = "Custom"
})

--[[

Title = Title of the Notification
Text = Text of the Notification
Icon = Icon of the Notification
Duration = Max amount of time the Notification will be shown on the screen
Theme = The theme of the Notificaion.

Notification Themes:
Success
Warning
Error
Information
Custom

  Creating your own theme :
Select Custom as a theme. Use the following options to change colors.
MainColor = Color3.fromRGB(255, 255, 255),
SideColor = Color3.fromRGB(255, 255, 255),
TitleColor = Color3.fromRGB(255, 255, 255),
TextColor = Color3.fromRGB(255, 255, 255),
IconColor = Color3.fromRGB(255, 255, 255),

Add these options in the Library:Notification function to change colors and create a custom theme.

]]
