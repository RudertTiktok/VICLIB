

---

## **How to Use the UI Library**

### **1. Loading the Library**
To use the library, you need to load it into your Roblox script using `loadstring` and `game:HttpGet`. Here's how to do it:

```lua
local VicLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/RudertTiktok/VICLIB/refs/heads/main/LIBRARYUI"))().__init
```

- **Note**: Replace the URL (`https://raw.githubusercontent.com/RudertTiktok/VICLIB/refs/heads/main/LIBRARYUI`) with the actual URL where your library is hosted.
- **Requirements**: Ensure `HttpService` is enabled in the game to allow `game:HttpGet` to fetch the library code.
- **Result**: After executing the above line, `VicLib` will contain the library object, ready to create UI elements.

### **2. Initializing the Library and Creating Tabs**
The library uses a tab-based structure with left and right sections for organizing UI elements. You initialize the library and create tabs using the `__init()` and `create_tab` functions. Here's a complete example:

```lua
-- Initialize the library
local Library = VicLib

-- Create tabs
local MainTab = Library:create_tab("Main")
local SettingsTab = Library:create_tab("Settings")
local VisualsTab = Library:create_tab("Visuals")

-- Example: Adding UI elements to tabs (detailed below)
```

- **Explanation**:
  - `Library.__init()`: Initializes the UI framework, creating a `ScreenGui` named "Rise" in `CoreGui`.
  - `create_tab(name)`: Creates a new tab with the specified name (e.g., "Main"). Each tab can contain elements in its left or right section.
  - Tabs are displayed in a scrolling frame on the left side of the UI, and clicking a tab shows its associated left and right sections.

### **3. Creating UI Elements**
The library supports various UI elements, each with specific parameters and functionality. Below is a comprehensive example showing how to create each type of element, along with explanations of their parameters and use cases.

#### **Complete Example**
```lua
-- Initialize the library
local Library = VicLib

-- Create tabs
local MainTab = Library.__init():create_tab("Main")
local SettingsTab = Library.__init():create_tab("Settings")
local VisualsTab = Library.__init():create_tab("Visuals")

-- Example 1: Toggle
MainTab:create_toggle({
    name = "Auto Click",
    section = "left",
    flag = "auto_click",
    enabled = false,
    callback = function(state)
        print("Auto Click is now: " .. tostring(state))
        -- Example: Toggle a game feature
        if state then
            -- Enable auto-click logic
        else
            -- Disable auto-click logic
        end
    end
})

-- Example 2: Toggle with Description
MainTab:create_description_toggle({
    name = "God Mode",
    description = "Makes you invincible",
    section = "right",
    flag = "god_mode",
    enabled = false,
    callback = function(state)
        print("God Mode is now: " .. tostring(state))
        -- Example: Toggle god mode
        if state then
            game.Players.LocalPlayer.Character.Humanoid.MaxHealth = math.huge
            game.Players.LocalPlayer.Character.Humanoid.Health = math.huge
        else
            game.Players.LocalPlayer.Character.Humanoid.MaxHealth = 100
            game.Players.LocalPlayer.Character.Humanoid.Health = 100
        end
    end
})

-- Example 3: Button
MainTab:create_button({
    name = "Reset Character",
    section = "left",
    callback = function()
        print("Resetting character...")
        game.Players.LocalPlayer.Character:BreakJoints()
    end
})

-- Example 4: Button with Description
MainTab:create_description_button({
    name = "Teleport to Spawn",
    description = "Teleports you to the spawn point",
    section = "right",
    callback = function()
        print("Teleporting to spawn...")
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 10, 0)
    end
})

-- Example 5: Slider
MainTab:create_slider({
    name = "Walk Speed",
    section = "left",
    flag = "walk_speed",
    value = 16,
    minimum_value = 16,
    maximum_value = 100,
    callback = function(value)
        print("Walk Speed set to: " .. value)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
    end
})

-- Example 6: Dropdown
MainTab:create_dropdown({
    name = "Select Weapon",
    section = "right",
    flag = "weapon_select",
    option = "Pistol",
    options = {"Pistol", "Rifle", "Shotgun", "Sniper"},
    callback = function(selected)
        print("Selected weapon: " .. selected)
        -- Example: Equip selected weapon
    end
})

-- Example 7: Textbox
SettingsTab:create_textbox({
    name = "Enter Username",
    section = "left",
    flag = "username",
    value = "",
    callback = function(text)
        print("Username entered: " .. text)
        -- Example: Update player's display name
        game.Players.LocalPlayer.DisplayName = text
    end
})

-- Example 8: Keybind
SettingsTab:create_keybind({
    name = "Toggle UI",
    section = "right",
    flag = "toggle_ui",
    keycode = Enum.KeyCode.F,
    callback = function(toggled)
        print("UI Toggled: " .. tostring(toggled))
        -- Example: Custom action on keybind toggle
    end
})

-- Example 9: Title
MainTab:create_title({
    name = "Main Features",
    section = "left"
})

-- Example 10: Paragraph
MainTab:create_paragraph({
    name = "About",
    title = "This is a custom UI library for Roblox.",
    section = "right"
})

-- Example 11: Verified Badge
MainTab:create_verified({
    title = "Trusted by users",
    section = "left"
})

-- Example 12: Line
MainTab:create_line({
    section = "left"
})

-- Example 13: Image
MainTab:create_image({
    section = "right",
    image = "rbxassetid://123456789" -- Replace with a valid image ID
})
```

#### **Explanation of Each Element**

1. **Toggle (`create_toggle`)**:
   - **Purpose**: Creates a checkbox-style toggle for enabling/disabling a feature.
   - **Parameters**:
     - `name`: The display name of the toggle (string).
     - `section`: "left" or "right" (string).
     - `flag`: Unique identifier for saving the toggle state (string).
     - `enabled`: Initial state (boolean, `true` or `false`).
     - `callback`: Function called when the toggle state changes (receives a boolean `state`).
   - **Behavior**: Clicking the toggle switches its state, updates the UI with animations (e.g., filling the checkbox), and saves the state to a file using `Library.save_flags()`.

2. **Toggle with Description (`create_description_toggle`)**:
   - **Purpose**: Similar to `create_toggle`, but includes a description text below the toggle name.
   - **Additional Parameter**:
     - `description`: Text displayed below the toggle name (string).
   - **Behavior**: Same as toggle, with additional descriptive text for clarity.

3. **Button (`create_button`)**:
   - **Purpose**: Creates a clickable button to trigger an action.
   - **Parameters**:
     - `name`: The display name of the button (string).
     - `section`: "left" or "right" (string).
     - `callback`: Function called when the button is clicked (no arguments).
   - **Behavior**: Clicking the button triggers the callback function.

4. **Button with Description (`create_description_button`)**:
   - **Purpose**: Similar to `create_button`, but includes a description text below the button name.
   - **Additional Parameter**:
     - `description`: Text displayed below the button name (string).
   - **Behavior**: Same as button, with additional descriptive text.

5. **Slider (`create_slider`)**:
   - **Purpose**: Creates a slider for selecting a numerical value within a range.
   - **Parameters**:
     - `name`: The display name of the slider (string).
     - `section`: "left" or "right" (string).
     - `flag`: Unique identifier for saving the slider value (string).
     - `value`: Initial value (number).
     - `minimum_value`: Minimum value of the slider (number).
     - `maximum_value`: Maximum value of the slider (number).
     - `callback`: Function called when the slider value changes (receives a number `value`).
   - **Behavior**: Dragging the slider updates the value, triggers the callback, and saves the state. The slider includes a visual fill and glow effect.

6. **Dropdown (`create_dropdown`)**:
   - **Purpose**: Creates a dropdown menu for selecting one option from a list.
   - **Parameters**:
     - `name`: The display name of the dropdown (string).
     - `section`: "left" or "right" (string).
     - `flag`: Unique identifier for saving the selected option (string).
     - `option`: Initial selected option (string).
     - `options`: List of available options (table of strings).
     - `callback`: Function called when an option is selected (receives a string `selected`).
   - **Behavior**: Clicking the dropdown toggles its options, and selecting an option updates the UI, triggers the callback, and saves the state.

7. **Textbox (`create_textbox`)**:
   - **Purpose**: Creates a text input field for user input.
   - **Parameters**:
     - `name`: Placeholder text for the textbox (string).
     - `section`: "left" or "right" (string).
     - `flag`: Unique identifier for saving the text (string).
     - `value`: Initial text (string).
     - `callback`: Function called when the text changes (receives a string `text`).
   - **Behavior**: Text entered is saved when the user presses Enter or loses focus, triggering the callback.

8. **Keybind (`create_keybind`)**:
   - **Purpose**: Creates a keybind for toggling a feature with a keyboard key.
   - **Parameters**:
     - `name`: The display name of the keybind (string).
     - `section`: "left" or "right" (string).
     - `flag`: Unique identifier for saving the keycode (string).
     - `keycode`: Initial key (Enum.KeyCode, e.g., `Enum.KeyCode.F`).
     - `callback`: Function called when the keybind is toggled (receives a boolean `toggled`).
   - **Behavior**: Clicking the keybind sets it to listen for a new key. Pressing the assigned key toggles the feature and triggers the callback.

9. **Title (`create_title`)**:
   - **Purpose**: Creates a text label for section headers.
   - **Parameters**:
     - `name`: The text to display (string).
     - `section`: "left" or "right" (string).
   - **Behavior**: Displays a static title with no interaction.

10. **Paragraph (`create_paragraph`)**:
    - **Purpose**: Creates a text block with a title and description.
    - **Parameters**:
      - `name`: The title text (string).
      - `title`: The description text (string).
      - `section`: "left" or "right" (string).
    - **Behavior**: Displays static text with a title and description.

11. **Verified Badge (`create_verified`)**:
    - **Purpose**: Creates a verified badge with text and an icon.
    - **Parameters**:
      - `title`: The description text (string).
      - `section`: "left" or "right" (string).
    - **Behavior**: Displays a static badge with text and an icon.

12. **Line (`create_line`)**:
    - **Purpose**: Creates a horizontal separator line.
    - **Parameters**:
      - `section`: "left" or "right" (string).
    - **Behavior**: Displays a static line to separate UI elements.

13. **Image (`create_image`)**:
    - **Purpose**: Displays an image in the UI.
    - **Parameters**:
      - `section`: "left" or "right" (string).
      - `image`: Asset ID of the image (string, e.g., "rbxassetid://123456789").
    - **Behavior**: Displays a static image with rounded corners.

### **4. Controlling the UI**
- **Opening/Closing the UI**:
  - By default, the UI toggles with `RightControl` (or `LeftControl` if `getgenv().Keycode_Enabled` is not set).
  - On mobile devices, a draggable button appears, which can be clicked to toggle the UI.
  - To customize the toggle key:
    ```lua
    getgenv().Keycode_Enabled = true
    -- Then, use RightControl to toggle (modify the library code to change the key if needed)
    ```

- **Dragging the UI**:
  - The UI can be dragged by clicking and holding on the `Container` frame, thanks to the `Library:drag()` function.

- **Saving/Loading Flags**:
  - The library automatically saves the state of toggles, sliders, dropdowns, textboxes, and keybinds to a file in the `Rise` folder (e.g., `Rise/{game.GameId}.lua`) using `Library.save_flags()` and `Library.load_flags()`.
  - States are persisted across sessions, making it easy to retain user settings.

- **Mobile Button Visibility**:
  - On mobile devices, a draggable button is visible by default. Press `LeftAlt` or `RightAlt` to toggle its visibility.
  - The button can be dragged to a new position, and its position animates smoothly using `TweenService`.

### **5. Notes and Best Practices**
- **Performance**:
  - Be cautious when adding many elements, as animations (e.g., `TweenService`) and loops (e.g., `task.spawn` in `AnimateGif`) can impact performance, especially on low-end devices.
  - Test the UI on different platforms (PC, mobile, controller) to ensure responsiveness.

- **Debugging**:
  - Use `print` statements in callbacks to verify that actions are triggered correctly.
  - Check the `Rise` folder in the game's workspace to ensure flags are saved correctly.

- **Customization**:
  - To change the UI's appearance, modify properties like `BackgroundColor3`, `UIGradient`, or `Image` in the library code.
  - Add sound effects or additional animations (e.g., hover effects) as suggested in the previous response for a more polished look.

- **Error Handling**:
  - Ensure valid image IDs are used for `create_image` and other image-based elements to avoid rendering issues.
  - Handle edge cases in callbacks (e.g., check if `LocalPlayer.Character` exists before modifying it).

### **6. Advanced Example**
For a more complex use case, here's an example of a UI for a game with combat, movement, and visual features:

```lua
local Library = VicLib

-- Create tabs
local CombatTab = Library.__init():create_tab("Combat")
local MovementTab = Library.__init():create_tab("Movement")
local VisualsTab = Library.__init():create_tab("Visuals")

-- Combat Tab
CombatTab:create_title({
    name = "Combat Features",
    section = "left"
})

CombatTab:create_toggle({
    name = "Aimbot",
    section = "left",
    flag = "aimbot",
    enabled = false,
    callback = function(state)
        print("Aimbot: " .. tostring(state))
        -- Add aimbot logic here
    end
})

CombatTab:create_button({
    name = "Kill All",
    section = "right",
    callback = function()
        print("Killing all players...")
        for _, player in pairs(game.Players:GetPlayers()) do
            if player ~= game.Players.LocalPlayer and player.Character then
                player.Character:BreakJoints()
            end
        end
    end
})

-- Movement Tab
MovementTab:create_title({
    name = "Movement Options",
    section = "left"
})

MovementTab:create_slider({
    name = "Jump Power",
    section = "left",
    flag = "jump_power",
    value = 50,
    minimum_value = 50,
    maximum_value = 200,
    callback = function(value)
        print("Jump Power set to: " .. value)
        if game.Players.LocalPlayer.Character then
            game.Players.LocalPlayer.Character.Humanoid.JumpPower = value
        end
    end
})

MovementTab:create_dropdown({
    name = "Teleport Location",
    section = "right",
    flag = "teleport_location",
    option = "Spawn",
    options = {"Spawn", "Base", "Safe Zone"},
    callback = function(selected)
        print("Teleporting to: " .. selected)
        local positions = {
            Spawn = CFrame.new(0, 10, 0),
            Base = CFrame.new(100, 10, 100),
            ["Safe Zone"] = CFrame.new(-100, 10, -100)
        }
        if game.Players.LocalPlayer.Character then
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = positions[selected]
        end
    end
})

-- Visuals Tab
VisualsTab:create_title({
    name = "Visual Settings",
    section = "left"
})

VisualsTab:create_textbox({
    name = "Custom Tag",
    section = "left",
    flag = "custom_tag",
    value = "Player",
    callback = function(text)
        print("Custom Tag set to: " .. text)
        game.Players.LocalPlayer.DisplayName = text
    end
})

VisualsTab:create_keybind({
    name = "Toggle ESP",
    section = "right",
    flag = "esp_toggle",
    keycode = Enum.KeyCode.E,
    callback = function(toggled)
        print("ESP Toggled: " .. tostring(toggled))
        -- Add ESP logic here
    end
})

VisualsTab:create_image({
    section = "right",
    image = "rbxassetid://123456789" -- Replace with a valid image ID
})
```

### **7. Conclusion**
This guide provides a complete overview of how to use your UI library, from loading it to creating and customizing UI elements. Each element is designed to be intuitive and flexible, with built-in animations and state persistence. If you need more specific examples (e.g., advanced animations, custom styling, or specific game integrations), let me know, and I can provide tailored code snippets!
