# AppleScript Reference for iTerm2

This guide covers the AppleScript fundamentals for automating iTerm2.

## iTerm2 Object Hierarchy

```
Application (iTerm2)
├── Window
│   ├── Tab
│   │   └── Session (Pane)
│   │       ├── Properties (colors, name, tty, etc.)
│   │       └── Commands (write, split, etc.)
│   └── Tab
│       └── Session
└── Window
    └── Tab
        └── Session
```

## Basic Pattern

All iTerm2 automation follows this pattern:

```applescript
tell application "iTerm2"
  -- Commands here
end tell
```

## Targeting Sessions

### Current Session

```applescript
tell application "iTerm2"
  tell current session of current tab of current window
    -- Commands for current pane
  end tell
end tell
```

### All Sessions in Tab

```applescript
tell application "iTerm2"
  tell current tab of current window
    repeat with aSession in sessions
      tell aSession
        -- Commands for each pane
      end tell
    end repeat
  end tell
end tell
```

### Specific Session by Index

```applescript
tell application "iTerm2"
  tell current tab of current window
    tell session 1
      -- Commands for first pane
    end tell
  end tell
end tell
```

## Pane Operations

### Split Pane

```applescript
-- Vertical split (new pane to the right)
tell current session of current tab of current window
  split vertically with default profile
end tell

-- Horizontal split (new pane below)
tell current session of current tab of current window
  split horizontally with default profile
end tell

-- Split with specific profile
tell current session of current tab of current window
  split vertically with profile "Development"
end tell
```

### Write Text

```applescript
tell current session of current tab of current window
  write text "echo Hello World"
end tell
```

## Tab Operations

### Create Tab

```applescript
tell current window
  create tab with default profile
end tell

-- With specific profile
tell current window
  create tab with profile "Development"
end tell
```

### Navigate Tabs

```applescript
tell current window
  select next tab
  select previous tab
  select tab 3  -- Go to tab 3
end tell
```

### Close Tab

```applescript
tell current tab of current window
  close
end tell
```

## Window Operations

### Create Window

```applescript
create window with default profile

-- With specific profile
create window with profile "Hotkey"
```

### Close Window

```applescript
tell current window
  close
end tell
```

## Color Operations

### Color Format

iTerm2 uses RGBA values where each component ranges from 0 to 65535:
- `{R, G, B, Alpha}`
- Alpha is usually 65535 (fully opaque)

### Converting Hex to iTerm2 Format

To convert hex RGB (00-FF) to iTerm2 (0-65535):

```
iTerm_value = hex_value * 257
```

Examples:
- `#000000` (black) → `{0, 0, 0, 65535}`
- `#FFFFFF` (white) → `{65535, 65535, 65535, 65535}`
- `#1a1a2e` (dark blue) → `{6682, 6682, 11822, 65535}`

### Setting Colors

```applescript
tell current session of current tab of current window
  -- Background color
  set background color to {0, 0, 0, 65535}

  -- Foreground (text) color
  set foreground color to {65535, 65535, 65535, 65535}

  -- Cursor color
  set cursor color to {65535, 0, 0, 65535}

  -- Selection color
  set selection color to {32768, 32768, 65535, 65535}
end tell
```

### Available Color Properties

- `background color`
- `foreground color`
- `cursor color`
- `cursor text color`
- `selection color`
- `selected text color`
- `ANSI black color`
- `ANSI red color`
- `ANSI green color`
- `ANSI yellow color`
- `ANSI blue color`
- `ANSI magenta color`
- `ANSI cyan color`
- `ANSI white color`
- `ANSI bright black color`
- (and other ANSI bright colors)

## Session Properties

### Get/Set Name

```applescript
tell current session of current tab of current window
  -- Set name
  set name to "My Session"

  -- Get name
  get name
end tell
```

### Set Profile

```applescript
tell current session of current tab of current window
  set profile name to "Development"
end tell
```

### Get Session Info

```applescript
tell current session of current tab of current window
  get tty        -- Terminal device path
  get id         -- Unique session ID
  get columns    -- Terminal width
  get rows       -- Terminal height
end tell
```

## Running AppleScript from Bash

Use `osascript` to run AppleScript from the command line:

```bash
# Inline script
osascript -e 'tell application "iTerm2" to activate'

# Multi-line script
osascript <<EOF
tell application "iTerm2"
  tell current session of current tab of current window
    split vertically with default profile
  end tell
end tell
EOF
```

## Error Handling

```applescript
try
  tell application "iTerm2"
    tell current session of current tab of current window
      split vertically with default profile
    end tell
  end tell
on error errMsg number errNum
  -- Handle error
  display dialog "Error: " & errMsg
end try
```

## Resources

- [iTerm2 Scripting Documentation](https://iterm2.com/documentation-scripting.html)
- [AppleScript Language Guide](https://developer.apple.com/library/archive/documentation/AppleScript/Conceptual/AppleScriptLangGuide/)
