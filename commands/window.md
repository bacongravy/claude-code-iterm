---
description: Manage iTerm2 windows - create, close, or list
argument-hint: [new|close|profile NAME]
allowed-tools: [Bash]
---

# Manage iTerm2 Windows

Create, close, or manage iTerm2 windows.

## Arguments

- `new`: Create a new window with the default profile
- `close`: Close the current window
- `profile NAME`: Create a new window with the specified profile

## Instructions

1. Parse the argument to determine the action.

2. Execute the appropriate AppleScript via osascript.

3. Do NOT output any commentary - just execute the AppleScript silently.

## AppleScript Reference

**Important**: The `create window` command returns a reference to the new window. Capture this reference to write commands to the new window's session.

```applescript
-- Create new window and cd to directory
tell application "iTerm2"
  set newWindow to (create window with default profile)
  tell current session of current tab of newWindow
    write text "cd /path/to/directory"
  end tell
end tell

-- Create new window with specific profile and cd
tell application "iTerm2"
  set newWindow to (create window with profile "ProfileName")
  tell current session of current tab of newWindow
    write text "cd /path/to/directory"
  end tell
end tell

-- Close current window
tell application "iTerm2"
  tell current window
    close
  end tell
end tell

-- List all windows (for debugging)
tell application "iTerm2"
  get windows
end tell
```
