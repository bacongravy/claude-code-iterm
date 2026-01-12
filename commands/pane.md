---
description: Split iTerm2 pane in current directory
argument-hint: [h|horizontal|v|vertical]
allowed-tools: [Bash]
---

# Split iTerm2 Pane

Create a new iTerm2 pane opened to the current working directory.

## Arguments

- No argument or `h` or `horizontal`: Split horizontally (new pane below)
- `v` or `vertical`: Split vertically (new pane to the right)

## Instructions

1. Parse the argument to determine split direction:
   - Default (no arg or `h` or `horizontal`): split horizontally
   - `v` or `vertical`: split vertically

2. Get the current working directory from the environment.

3. Execute via osascript:
   - Split the current session with the chosen direction
   - Write `cd <cwd>` to the new pane

4. Do NOT output any commentary - just execute the AppleScript silently.

## AppleScript Reference

```applescript
-- Vertical split (new pane to the right)
tell application "iTerm2"
  tell current session of current tab of current window
    split vertically with default profile
  end tell
end tell

-- Horizontal split (new pane below)
tell application "iTerm2"
  tell current session of current tab of current window
    split horizontally with default profile
  end tell
end tell

-- Navigate to directory in new pane
tell application "iTerm2"
  tell current session of current tab of current window
    write text "cd /path/to/directory"
  end tell
end tell
```
