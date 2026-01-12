---
description: Manage iTerm2 tabs - create, close, navigate, or rename
argument-hint: [new|close|next|prev|goto N|rename NAME]
allowed-tools: [Bash]
---

# Manage iTerm2 Tabs

Create, close, navigate between, or rename iTerm2 tabs.

## Arguments

- `new`: Create a new tab in the current window
- `close`: Close the current tab
- `next`: Switch to the next tab
- `prev`: Switch to the previous tab
- `goto N`: Switch to tab number N (1-indexed)
- `rename NAME`: Rename the current tab to NAME

## Instructions

1. Parse the argument to determine the action.

2. Execute the appropriate AppleScript via osascript.

3. Do NOT output any commentary - just execute the AppleScript silently.

## AppleScript Reference

**Important**: The `create tab` command returns a reference to the new tab. Capture this reference to write commands to the new tab's session.

```applescript
-- Create new tab and cd to directory
tell application "iTerm2"
  tell current window
    set newTab to (create tab with default profile)
  end tell
  tell current session of newTab
    write text "cd /path/to/directory"
  end tell
end tell

-- Close current tab
tell application "iTerm2"
  tell current tab of current window
    close
  end tell
end tell

-- Switch to next tab
tell application "iTerm2"
  tell current window
    select next tab
  end tell
end tell

-- Switch to previous tab
tell application "iTerm2"
  tell current window
    select previous tab
  end tell
end tell

-- Switch to specific tab (N is tab index, 1-based)
tell application "iTerm2"
  tell current window
    select tab N
  end tell
end tell

-- Rename current tab
tell application "iTerm2"
  tell current session of current tab of current window
    set name to "Tab Name"
  end tell
end tell
```
