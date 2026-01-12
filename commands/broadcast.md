---
description: Toggle iTerm2 broadcast input mode
argument-hint: [on|off|toggle]
allowed-tools: [Bash]
---

# Toggle iTerm2 Broadcast Input

Enable or disable broadcast input mode, which sends keystrokes to multiple panes simultaneously.

## Arguments

- `on`: Enable broadcast to all panes in current tab
- `off`: Disable broadcast mode
- `toggle`: Toggle broadcast mode (default if no argument)

## Instructions

1. Parse the argument to determine the action (default: toggle).

2. Use System Events to simulate the keyboard shortcut since broadcast is not directly scriptable via AppleScript:
   - Cmd+Shift+I: Toggle broadcast to all panes in current tab
   - Or use the Shell Integration menu

3. Do NOT output any commentary - just execute silently.

## Implementation

Since iTerm2's broadcast feature is not directly accessible via AppleScript, use keyboard simulation:

```applescript
-- Toggle broadcast input (Cmd+Shift+I)
tell application "iTerm2" to activate
tell application "System Events"
  keystroke "i" using {command down, shift down}
end tell
```

## Alternative: Shell Menu Approach

```applescript
-- Via menu (more reliable)
tell application "iTerm2" to activate
tell application "System Events"
  tell process "iTerm2"
    click menu item "Toggle Broadcast Input to Current Session" of menu "Shell" of menu bar 1
  end tell
end tell
```

## Notes

- Requires accessibility permissions for System Events
- First-time use will prompt for permissions in System Preferences
- Broadcast is indicated by a red border around broadcasting panes
- Useful for running the same commands on multiple servers
