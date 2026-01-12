---
description: Send a command to an iTerm2 pane
argument-hint: [COMMAND|--all COMMAND]
allowed-tools: [Bash]
---

# Send Command to iTerm2 Pane

Execute a command in the current pane or all panes in the current tab.

## Arguments

- `COMMAND`: Send the command to the current pane
- `--all COMMAND`: Send the command to all panes in the current tab

## Instructions

1. Parse the argument to determine:
   - Whether to send to all panes (--all flag)
   - The command to execute

2. Execute AppleScript to write the command to the appropriate session(s).

3. Do NOT output any commentary - just execute the AppleScript silently.

## AppleScript Reference

```applescript
-- Send command to current pane
tell application "iTerm2"
  tell current session of current tab of current window
    write text "your-command-here"
  end tell
end tell

-- Send command to all panes in current tab
tell application "iTerm2"
  tell current tab of current window
    repeat with aSession in sessions
      tell aSession
        write text "your-command-here"
      end tell
    end repeat
  end tell
end tell
```

## Examples

| Input | Action |
|-------|--------|
| `npm start` | Run npm start in current pane |
| `--all clear` | Clear all panes |
| `--all cd ~/projects` | Navigate all panes to projects folder |
| `git status` | Show git status in current pane |

## Notes

- Commands are executed as if typed by the user
- Each command is followed by a newline (like pressing Enter)
- Use quotes for commands with spaces: `"echo hello world"`
- For complex commands, consider using broadcast mode instead
