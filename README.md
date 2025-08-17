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

How To Use VicLib?

```lua
local gui = Library:new()
local mainTab = gui:create_tab("Main")
local module = mainTab:create_module({ title = "Settings", section = "left" })
local checkbox = mainTab:create_checkbox({
    name = "Enable ESP",
    section = "left",
    flag = "esp_enabled",
    enabled = false,
    desc = "Toggles ESP to highlight players through walls",
    callback = function(state)
        print("ESP " .. (state and "Enabled" or "Disabled"))
    end
})
local toggle = mainTab:create_toggle({
    name = "Auto Click",
    section = "right",
    flag = "auto_click",
    enabled = false,
    desc = "Automatically clicks for you",
    callback = function(state)
        print("Auto Click " .. (state and "On" or "Off"))
    end
})
local slider = mainTab:create_slider({
    name = "Speed",
    section = "left",
    flag = "speed_value",
    min = 0,
    max = 100,
    value = 50,
    desc = "Adjusts movement speed (0-100)",
    callback = function(value)
        print("Speed set to " .. value)
    end
})
local dropdown = mainTab:create_dropdown({
    name = "Mode",
    section = "right",
    flag = "mode_select",
    options = {"Normal", "Hard", "Extreme"},
    value = "Normal",
    desc = "Selects game difficulty mode",
    callback = function(value)
        print("Mode set to " .. value)
    end
})
local textbox = mainTab:create_textbox({
    name = "Player Name",
    section = "left",
    flag = "player_name",
    value = "",
    desc = "Enter a custom player name",
    callback = function(text)
        print("Player name set to " .. text)
    end
})
local keybind = mainTab:create_keybind({
    name = "Action Key",
    section = "right",
    flag = "action_key",
    keycode = Enum.KeyCode.F,
    desc = "Key to trigger a special action",
    callback = function(key)
        print("Action key pressed: " .. key)
    end
})```
