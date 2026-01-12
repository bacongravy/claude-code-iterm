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

```applescript
-- Create new window with default profile
tell application "iTerm2"
  create window with default profile
end tell

-- Create new window with specific profile
tell application "iTerm2"
  create window with profile "ProfileName"
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
