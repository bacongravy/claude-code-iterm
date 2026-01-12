---
description: Change iTerm2 colors - dark, light, or custom
argument-hint: [dark|light|bg RRGGBB|fg RRGGBB]
allowed-tools: [Bash]
---

# Change iTerm2 Theme/Colors

Quickly change the terminal colors for the current session.

## Arguments

- `dark`: Apply dark theme (black background, white text)
- `light`: Apply light theme (white background, black text)
- `bg RRGGBB`: Set custom background color (hex RGB)
- `fg RRGGBB`: Set custom foreground color (hex RGB)

## Instructions

1. Parse the argument to determine the color action.

2. For hex colors (RRGGBB format), convert to iTerm2's format:
   - iTerm2 uses values 0-65535 for each RGB component
   - Convert hex (00-FF) to 0-65535 scale: `hex_value * 257`

3. Execute AppleScript to set the colors.

4. Do NOT output any commentary - just execute the AppleScript silently.

## Color Presets

| Theme | Background | Foreground |
|-------|------------|------------|
| dark  | 000000     | FFFFFF     |
| light | FFFFFF     | 000000     |

## AppleScript Reference

```applescript
-- Set background color (values 0-65535 for each RGB + Alpha)
tell application "iTerm2"
  tell current session of current tab of current window
    set background color to {0, 0, 0, 65535}
  end tell
end tell

-- Set foreground color
tell application "iTerm2"
  tell current session of current tab of current window
    set foreground color to {65535, 65535, 65535, 65535}
  end tell
end tell

-- Example: Dark theme
tell application "iTerm2"
  tell current session of current tab of current window
    set background color to {0, 0, 0, 65535}
    set foreground color to {65535, 65535, 65535, 65535}
  end tell
end tell

-- Example: Light theme
tell application "iTerm2"
  tell current session of current tab of current window
    set background color to {65535, 65535, 65535, 65535}
    set foreground color to {0, 0, 0, 65535}
  end tell
end tell
```

## Hex to iTerm2 Conversion

To convert hex RRGGBB to iTerm2 format:
```
R = parseInt(RR, 16) * 257
G = parseInt(GG, 16) * 257
B = parseInt(BB, 16) * 257
Alpha = 65535
```

Example: `1a1a2e` (dark blue)
- R: 0x1a = 26 * 257 = 6682
- G: 0x1a = 26 * 257 = 6682
- B: 0x2e = 46 * 257 = 11822
- Result: `{6682, 6682, 11822, 65535}`
