---
description: Create iTerm2 pane layouts for development workflows
argument-hint: [grid|sidebar|stack|dev]
allowed-tools: [Bash]
---

# Create iTerm2 Layouts

Create preset pane layouts optimized for common development workflows.

## Arguments

- `grid`: 2x2 grid layout (4 equal panes)
- `sidebar`: Main pane with narrow sidebar on the right
- `stack`: Main pane with two smaller panes stacked below
- `dev`: Development layout - main editor area + terminal below + logs sidebar

## Layout Diagrams

### grid (2x2)
```
┌─────────┬─────────┐
│    1    │    2    │
├─────────┼─────────┤
│    3    │    4    │
└─────────┴─────────┘
```

### sidebar
```
┌──────────────┬────┐
│              │    │
│     Main     │Side│
│              │    │
└──────────────┴────┘
```

### stack
```
┌────────────────────┐
│       Main         │
├──────────┬─────────┤
│    2     │    3    │
└──────────┴─────────┘
```

### dev
```
┌──────────────┬────┐
│              │    │
│    Editor    │Logs│
│              │    │
├──────────────┴────┤
│     Terminal      │
└───────────────────┘
```

## Instructions

1. Parse the argument to determine which layout to create.

2. Execute a series of AppleScript commands to create the layout:
   - Split panes in the correct sequence
   - Optionally set names for each pane

3. Navigate all panes to the current working directory.

4. Do NOT output any commentary - just execute the AppleScript silently.

## AppleScript Reference

```applescript
-- Grid layout (2x2)
tell application "iTerm2"
  tell current session of current tab of current window
    -- Split vertically (creates pane 2)
    split vertically with default profile
  end tell
  tell current tab of current window
    -- Select first session and split horizontally (creates pane 3)
    tell session 1
      split horizontally with default profile
    end tell
    -- Select second session and split horizontally (creates pane 4)
    tell session 2
      split horizontally with default profile
    end tell
  end tell
end tell

-- Sidebar layout
tell application "iTerm2"
  tell current session of current tab of current window
    split vertically with default profile
  end tell
end tell

-- Stack layout
tell application "iTerm2"
  tell current session of current tab of current window
    split horizontally with default profile
  end tell
  -- Split the bottom pane vertically
  tell current tab of current window
    tell session 2
      split vertically with default profile
    end tell
  end tell
end tell

-- Dev layout (main + logs sidebar + terminal below)
tell application "iTerm2"
  tell current session of current tab of current window
    -- First split horizontally (terminal below)
    split horizontally with default profile
    -- Then split the top pane vertically (logs sidebar)
    split vertically with default profile
  end tell
end tell
```

## Navigate All Panes to Directory

After creating a layout, use this pattern to cd all panes to the current directory:

```applescript
tell application "iTerm2"
  tell current tab of current window
    repeat with aSession in sessions
      tell aSession
        write text "cd /path/to/directory"
      end tell
    end repeat
  end tell
end tell
```

## Notes

- Layouts start from the current pane and create new panes relative to it
- New panes do NOT automatically inherit the working directory - use the pattern above
- Pane proportions can be adjusted manually after creation
