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

**Important**: The `split` command returns a reference to the new session. You must capture this reference and use it to write commands to the new pane. Otherwise, commands will be sent to the original pane.

```applescript
-- Vertical split (new pane to the right) with cd
tell application "iTerm2"
  tell current session of current tab of current window
    set newSession to (split vertically with default profile)
  end tell
  tell newSession
    write text "cd /path/to/directory"
  end tell
end tell

-- Horizontal split (new pane below) with cd
tell application "iTerm2"
  tell current session of current tab of current window
    set newSession to (split horizontally with default profile)
  end tell
  tell newSession
    write text "cd /path/to/directory"
  end tell
end tell
```
