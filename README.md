markdown
# VicNotify Usage

VicNotify is a Roblox Lua notification library for creating customizable notifications (`error`, `info`, `message`, `success`, `warning`).

## Installation
Load the library in your Roblox script:

```lua
local Notification = loadstring(game:HttpGet("https://raw.githubusercontent.com/RudertTiktok/VICLIB/refs/heads/main/VICNOTIFY", true))()
```

**Note**: Ensure the URL is valid. Host locally if inaccessible.

## Creating a Notification
Use `Notification.new` to create a notification:

```lua
Notification.new(type, heading, body, autoRemove, autoRemoveTime, onCloseFunction)
```

- `type` (string): `error`, `info`, `message`, `success`, or `warning`.
- `heading` (string): Notification title.
- `body` (string): Notification message.
- `autoRemove` (boolean, optional): Auto-close after `autoRemoveTime` (default: false).
- `autoRemoveTime` (number, optional): Seconds before auto-close (default: 5).
- `onCloseFunction` (function, optional): Callback when notification closes.

**Example**:
```lua
Notification.new("error", "Error", "Something went wrong!", true, 3)
Notification.new("success", "Success", "Task done.", true, 4)
Notification.new("info", "Info", "Test message.")
Notification.new("warning", "Warning", "Be cautious.", true, 5)
Notification.new("message", "Message", "Hello!", true, 4, function() print("Closed!") end)
```

## Modifying Notifications
Notifications return an object with these methods:

- `changeHeading(newHeading)`: Update title.
- `changeBody(newBody)`: Update message (auto-resizes).
- `changeColor(primary, secondary, textColor)`: Change colors (Color3 values).
- `deleteTimeout(waitTime)`: Close after delay (default: 3 seconds).
- `delete()`: Close immediately.

**Example**:
```lua
local notif = Notification.new("success", "Success", "Task completed.")
notif:changeHeading("New Title")
notif:changeBody("Updated message with resizing.")
notif:changeColor(Color3.fromRGB(200, 200, 200), Color3.fromRGB(100, 100, 100), Color3.fromRGB(255, 255, 255))
notif:deleteTimeout(2) -- Closes after 2 seconds
-- notif:delete() -- Closes immediately
```
```

### Notes
- **Concise Focus**: Only includes installation and usage (creating/modifying notifications), omitting troubleshooting, features, or other details as requested.
- **URL**: Uses the provided URL. Replace with your actual repository URL if different.
- **Examples**: Mirrors the structure of your example code, showing all notification types and modification methods.
- **Dynamic Resizing**: Noted in `changeBody` to reflect the updated code’s feature.

Let me know if you need further adjustments or a different format!

---

## **How to Use the VicLib UI Library**

This guide explains how to use the `VicLib` UI library to create a customizable graphical user interface (GUI) in Roblox. The library supports tabs, toggles, buttons, sliders, dropdowns, textboxes, keybinds, images, and more, with animations and persistent state saving. The structure is designed to be beginner-friendly, with clear examples and explanations to help anyone use the library effectively.

### **1. Loading the Library**
To use `VicLib`, load it into your Roblox script using `loadstring` and `game:HttpGet`. Here’s how:

```lua
local VicLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/RudertTiktok/VICLIB/refs/heads/main/VicLib.txt"))().__init
```

- **Note**: Ensure the URL (`https://raw.githubusercontent.com/RudertTiktok/VICLIB/refs/heads/main/VicLib.txt`) is correct and accessible. This fetches the library code from GitHub.
- **Requirements**: `HttpService` must be enabled in the game to allow `game:HttpGet`.
- **Result**: After running this line, `VicLib` is a table containing methods to create the GUI. A `ScreenGui` named "Rise" is created in `game.CoreGui`, displaying a window with a top bar, tab list, and sections for UI elements.

### **2. Initializing the Library and Creating Tabs**
The library organizes UI elements in tabs, each with left and right sections. You initialize the library with `__init` and create tabs using `create_tab`. Here’s a basic example:

```lua
local VicLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/RudertTiktok/VICLIB/refs/heads/main/VicLib.txt"))().__init

-- Create tabs
local MainTab = VicLib.create_tab("Main")
local SettingsTab = VicLib.create_tab("Settings")
local VisualsTab = VicLib.create_tab("Visuals")
```

- **Explanation**:
  - `__init()`: Sets up the GUI framework, creating the main window with a top bar (showing "Frostware" and a timer) and a tab list on the left.
  - `create_tab(name)`: Creates a tab with the specified name (e.g., "Main"). Each tab has a left and right `ScrollingFrame` for placing UI elements.
  - Tabs appear in a vertical list on the left side of the GUI. Clicking a tab shows its sections, hiding others with smooth animations.

### **3. Creating UI Elements**
`VicLib` supports various UI elements, each added to a tab’s left or right section. Below is a complete example showing how to create each element, followed by detailed explanations.

#### **Complete Example**
This example creates a GUI with multiple tabs and various UI elements, similar to what you might use in a game like "Blade Ball":

```lua
local VicLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/RudertTiktok/VICLIB/refs/heads/main/VicLib.txt"))().__init

-- Create tabs
local HomeTab = VicLib.create_tab("Home")
local CombatTab = VicLib.create_tab("Combat")
local SettingsTab = VicLib.create_tab("Settings")

-- Home Tab
HomeTab.create_title({
    name = "Welcome",
    section = "left"
})

HomeTab.create_paragraph({
    name = "About",
    title = "This is a GUI for Blade Ball.",
    section = "right"
})

HomeTab.create_image({
    section = "left",
    image = "rbxassetid://123456789" -- Replace with a valid image ID
})

-- Combat Tab
CombatTab.create_title({
    name = "Combat Features",
    section = "left"
})

CombatTab.create_toggle({
    name = "Auto Parry",
    section = "left",
    flag = "auto_parry",
    enabled = false,
    callback = function(state)
        print("Auto Parry: " .. tostring(state))
        -- Add auto-parry logic here
    end
})

CombatTab.create_description_toggle({
    name = "Manual Spam",
    description = "Enables manual spamming GUI",
    section = "right",
    flag = "manual_spam",
    enabled = false,
    callback = function(state)
        print("Manual Spam: " .. tostring(state))
        -- Add manual spam logic here
    end
})

CombatTab.create_slider({
    name = "Parry Delay",
    section = "left",
    flag = "parry_delay",
    value = 0.5,
    minimum_value = 0,
    maximum_value = 2,
    callback = function(value)
        print("Parry Delay: " .. value)
        -- Adjust parry timing
    end
})

CombatTab.create_dropdown({
    name = "Curve Position",
    section = "right",
    flag = "curve_position",
    option = "Custom",
    options = {"Custom", "Random", "Backwards", "Straight"},
    callback = function(selected)
        print("Curve Position: " .. selected)
        -- Adjust ball curve logic
    end
})

CombatTab.create_button({
    name = "Reset Game",
    section = "left",
    callback = function()
        print("Resetting game...")
        game:GetService("Players").LocalPlayer:Kick("Resetting...")
    end
})

-- Settings Tab
SettingsTab.create_title({
    name = "Settings",
    section = "left"
})

SettingsTab.create_textbox({
    name = "Enter Code",
    section = "left",
    flag = "code",
    value = "",
    callback = function(text)
        print("Code: " .. text)
        -- Process code input
    end
})

SettingsTab.create_keybind({
    name = "Toggle Auto Parry",
    section = "right",
    flag = "parry_key",
    keycode = Enum.KeyCode.E,
    callback = function(toggled)
        print("Auto Parry Toggled: " .. tostring(toggled))
        -- Toggle auto-parry feature
    end
})

SettingsTab.create_verified({
    title = "Trusted by players",
    section = "left"
})

SettingsTab.create_line({
    section = "right"
})
```

#### **Explanation of Each Element**

1. **Title (`create_title`)**:
   - **Purpose**: Adds a text label to label a section.
   - **Parameters**:
     - `name` (string): The text to display (e.g., "Welcome").
     - `section` (string): `"left"` or `"right"`.
   - **Behavior**: Displays a static `TextLabel` with the Montserrat font, used for organizing UI elements.
   - **Example Use**: Labeling sections like "Combat Features" or "Settings".

2. **Toggle (`create_toggle`)**:
   - **Purpose**: Creates a checkbox for enabling/disabling a feature.
   - **Parameters**:
     - `name` (string): Toggle label (e.g., "Auto Parry").
     - `section` (string): `"left"` or `"right"`.
     - `flag` (string): Unique identifier for saving the state (e.g., "auto_parry").
     - `enabled` (boolean): Initial state (`true` or `false`).
     - `callback` (function): Called with the new state (`true` or `false`) when toggled.
   - **Behavior**: Clicking toggles the state, updates `Library.Flags[flag]`, saves to a file, and animates the checkbox (shows/hides checkmark). The callback is triggered with the new state.
   - **Example Use**: Enabling/disabling auto-parry in a game.

3. **Description Toggle (`create_description_toggle`)**:
   - **Purpose**: Like a toggle, but with a description below the name.
   - **Parameters**:
     - Same as `create_toggle`, plus:
     - `description` (string): Text shown below the toggle (e.g., "Enables manual spamming GUI").
   - **Behavior**: Same as toggle, with an additional `TextLabel` for the description in a lighter color (RGB 170, 170, 170).
   - **Example Use**: Providing context for complex features like manual spam.

4. **Button (`create_button`)**:
   - **Purpose**: Creates a clickable button to perform an action.
   - **Parameters**:
     - `name` (string): Button label (e.g., "Reset Game").
     - `section` (string): `"left"` or `"right"`.
     - `callback` (function): Called when clicked (no arguments).
   - **Behavior**: Clicking triggers the callback. The button includes a label and an icon.
   - **Example Use**: Resetting the game or copying a link.

5. **Description Button (`create_description_button`)**:
   - **Purpose**: Like a button, but with a description.
   - **Parameters**:
     - Same as `create_button`, plus:
     - `description` (string): Text shown below the button.
   - **Behavior**: Same as button, with an additional description `TextLabel`.
   - **Example Use**: Buttons with extra context, like copying a Discord link.

6. **Slider (`create_slider`)**:
   - **Purpose**: Allows selecting a numeric value within a range.
   - **Parameters**:
     - `name` (string): Slider label (e.g., "Parry Delay").
     - `section` (string): `"left"` or `"right"`.
     - `flag` (string): Identifier for saving the value (e.g., "parry_delay").
     - `value` (number): Initial value (e.g., 0.5).
     - `minimum_value` (number): Minimum value (e.g., 0).
     - `maximum_value` (number): Maximum value (e.g., 2).
     - `callback` (function): Called with the new value (number) when moved.
   - **Behavior**: Dragging updates the value, saves to `Library.Flags[flag]`, and triggers the callback. The slider has a visual fill and glow effect, with the value displayed.
   - **Example Use**: Adjusting parry timing or walk speed.

7. **Dropdown (`create_dropdown`)**:
   - **Purpose**: Allows selecting an option from a list.
   - **Parameters**:
     - `name` (string): Dropdown label (e.g., "Curve Position").
     - `section` (string): `"left"` or `"right"`.
     - `flag` (string): Identifier for saving the selection (e.g., "curve_position").
     - `option` (string): Initial option (e.g., "Custom").
     - `options` (table): List of options (e.g., `{"Custom", "Random", "Backwards", "Straight"}`).
     - `callback` (function): Called with the selected option (string) when changed.
   - **Behavior**: Clicking toggles the option list with animations. Selecting an option updates `Library.Flags[flag]`, saves, and triggers the callback.
   - **Example Use**: Choosing ball curve positions in a game.

8. **Textbox (`create_textbox`)**:
   - **Purpose**: Allows entering custom text.
   - **Parameters**:
     - `name` (string): Placeholder text (e.g., "Enter Code").
     - `section` (string): `"left"` or `"right"`.
     - `flag` (string): Identifier for saving the text (e.g., "code").
     - `value` (string): Initial text (e.g., "").
     - `callback` (function): Called with the entered text (string) when focus is lost.
   - **Behavior**: Text is saved to `Library.Flags[flag]` and the callback is triggered when the user presses Enter or loses focus.
   - **Example Use**: Entering redeem codes or player names.

9. **Keybind (`create_keybind`)**:
   - **Purpose**: Assigns a key to toggle a feature.
   - **Parameters**:
     - `name` (string): Keybind label (e.g., "Toggle Auto Parry").
     - `section` (string): `"left"` or `"right"`.
     - `flag` (string): Identifier for saving the key (e.g., "parry_key").
     - `keycode` (Enum.KeyCode): Default key (e.g., `Enum.KeyCode.E`).
     - `callback` (function): Called with the toggled state (`true` or `false`) when the key is pressed.
   - **Behavior**: Clicking sets the keybind to listen for a new key (shows "..."). Pressing the assigned key toggles the state, saves to `Library.Flags[flag]`, and triggers the callback.
   - **Example Use**: Toggling auto-parry with a keypress.

10. **Paragraph (`create_paragraph`)**:
    - **Purpose**: Displays a title and description text.
    - **Parameters**:
      - `name` (string): Title text (e.g., "About").
      - `title` (string): Description text (e.g., "This is a GUI for Blade Ball.").
      - `section` (string): `"left"` or `"right"`.
    - **Behavior**: Shows static text with a title and description, no interaction.
    - **Example Use**: Displaying information or credits.

11. **Verified Badge (`create_verified`)**:
    - **Purpose**: Shows a verified badge with text and an icon.
    - **Parameters**:
      - `title` (string): Description text (e.g., "Trusted by players").
      - `section` (string): `"left"` or `"right"`.
    - **Behavior**: Displays a static badge with text and an icon, no interaction.
    - **Example Use**: Indicating trusted status.

12. **Line (`create_line`)**:
    - **Purpose**: Adds a horizontal separator line.
    - **Parameters**:
      - `section` (string): `"left"` or `"right"`.
    - **Behavior**: Shows a static line to separate UI elements.
    - **Example Use**: Organizing UI sections visually.

13. **Image (`create_image`)**:
    - **Purpose**: Displays an image.
    - **Parameters**:
      - `section` (string): `"left"` or `"right"`.
      - `image` (string): Roblox asset ID (e.g., "rbxassetid://123456789").
    - **Behavior**: Shows a static image with rounded corners, no interaction.
    - **Example Use**: Displaying a game logo or screenshot.

### **4. Controlling the UI**

- **Toggling the UI**:
  - **Default Key**: Press `RightControl` (or `LeftControl` if `getgenv().Keycode_Enabled` is not set) to show/hide the GUI.
  - **Mobile Button**: On mobile devices, a draggable button appears at the bottom-right. Click it to toggle the GUI.
  - **Customizing the Toggle Key**:
    ```lua
    getgenv().Keycode_Enabled = true
    -- Uses RightControl by default. Modify the library code to change the key.
    ```

- **Dragging the UI**:
  - Click and hold the main window (`Container`) to drag it. The position updates smoothly with `TweenService`.

- **Mobile Button Controls**:
  - **Visibility**: Press `LeftAlt` or `RightAlt` to show/hide the mobile button.
  - **Dragging**: Drag the mobile button to reposition it.
  - **Position Shortcuts** (PC only):
    - Press `Ctrl + C + P` to move the mobile button to the center.
    - Press `Ctrl + C + B` to reset it to the default position.

- **Saving/Loading States**:
  - The library saves toggle, slider, dropdown, textbox, and keybind states to a file in the `Rise` folder (`Rise/{game.GameId}.lua`) using `Library.save_flags()` and `Library.load_flags()`.
  - States persist across game sessions, restoring user settings automatically.

### **5. Notes and Best Practices**

- **Performance**:
  - Adding many elements may impact performance due to animations (`TweenService`) and loops (e.g., GIF animation in `AnimateGif`). Test on low-end devices to ensure smoothness.
  - Limit the number of active animations for better performance.

- **Debugging**:
  - Use `print` in callbacks to verify functionality (e.g., `print("Toggle state: " .. state)`).
  - Check the `Rise` folder in the Roblox workspace to confirm flag saving.
  - Ensure valid image IDs for `create_image` to avoid rendering issues.

- **Customization**:
  - Modify the library’s `BackgroundColor3`, `UIGradient`, or `Image` properties to change the GUI’s appearance.
  - Add sound effects for clicks or hover effects to enhance user experience:
    ```lua
    -- Example: Add click sound to toggle
    toggle.MouseButton1Click:Connect(function()
        local sound = Instance.new("Sound", game.SoundService)
        sound.SoundId = "rbxassetid://123456789" -- Replace with sound ID
        sound:Play()
    end)
    ```

- **Error Handling**:
  - Check for `LocalPlayer.Character` existence in callbacks to avoid errors:
    ```lua
    callback = function(value)
        if game.Players.LocalPlayer.Character then
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
        end
    end
    ```
  - Handle invalid inputs in textboxes or sliders to prevent crashes.

- **Cross-Platform Testing**:
  - Test the GUI on PC, mobile, and controller to ensure compatibility. The library auto-detects the device type (`PC`, `Mobile`, `Controller`) and adjusts visibility of the mobile button.

### **6. Advanced Example**
Here’s a more complex example for a "Blade Ball" GUI, integrating multiple features:

```lua
local VicLib = loadstring(game:HttpGet('https://raw.githubusercontent.com/RudertTiktok/VICLIB/refs/heads/main/VicLib.txt'))()
local main = VicLib.new()
local tab = main.create_tab('Main')

tab.create_title({
	name = 'AutoParry',
	section = 'left'
})
tab.create_toggle({
	name = 'Enabled',
	flag = 'autoparry',

	section = 'left',
	enabled = false,

	callback = function(state: boolean)
		print(`{state}`)
	end
})
tab.create_dropdown({
	name = 'Direction',
	flag = 'Direction',
	section = 'left',

	option = 'Custom',
	options = {'Custom', 'High', 'Random'},

	callback = function(value: string)
		print(value)
	end
})
tab.create_title({
	name = 'Visualizer',
	section = 'right'
})
tab.create_toggle({
	name = 'Enabled',
	flag = 'visualise',

	section = 'right',
	enabled = false,

	callback = function(state: boolean)
	print(`{state}`)
	end
})
tab.create_title({
	name = 'HitSound',
	section = 'left'
})
tab.create_toggle({
	name = 'Enabled',
	flag = 'hitsound',

	section = 'left',
	enabled = false,

	callback = function(state: boolean)
		print(`{state}`)
	end
})
tab.create_dropdown({
	name = 'Sound',
	flag = 'soundpick',
	section = 'left',

	option = 'Neverlose',
	options = {'Click', 'Neverlose', 'Bonk'},

	callback = function(value: string)
		print(value)
	end
})
tab.create_title({
	name = 'AI',
	section = 'right'
})
tab.create_toggle({
	name = 'Enabled',
	flag = 'AI',

	section = 'right',
	enabled = false,

	callback = function(state: boolean)
    print(`{state}`)
	end
})
tab.create_title({
	name = 'Spin',
	section = 'right'
})
tab.create_toggle({
	name = 'Enabled',
	flag = 'spin',

	section = 'right',
	enabled = false,

	callback = function(state: boolean)
		print(`{state}`)
	end
})
tab.create_slider({
	name = 'Speed',
	flag = 'spinspeed',

	section = 'right',

	value = 25,
	minimum_value = 0,
	maximum_value = 100,

	callback = function(value: number)
		print(value)
	end
})
tab.create_title({
	name = 'Auto Open Crate',
	section = 'left'
})
tab.create_toggle({
	name = 'Enabled',
	flag = 'swordbox',

	section = 'left',
	enabled = false,

	callback = function(state: boolean)
		print(`{state}`)
	end
})
tab.create_dropdown({
	name = 'Crate',
	flag = 'selectbox',
	section = 'left',

	option = 'Sword Crate',
	options = {'Explosion Crate', 'Sword Crate'},

	callback = function(value: string)
		print(value)
	end
})
tab.create_title({
	name = 'Auto Rewards',
	section = 'right'
})
tab.create_toggle({
	name = 'Enabled',
	flag = 'rewarde',

	section = 'right',
	enabled = false,

	callback = function(state: boolean)
		print(`{state}`)
	end
})
tab.create_dropdown({
	name = 'Rewards',
	flag = 'selectrewards',
	section = 'right',

	option = 'Playtime Rewards',
	options = {'Playtime Rewards', 'Clan Rewards', 'Login Rewards', 'All'},

	callback = function(value: string)
	    print(value)
	end
})
return library
```
