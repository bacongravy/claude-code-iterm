---
name: iterm
description: Comprehensive iTerm2 terminal automation. Use for managing panes, tabs, windows, profiles, colors, and multi-pane workflows on macOS.
allowed-tools:
  - Bash(osascript:*)
---

# iTerm2 Automation Skill

Automate iTerm2 terminal operations on macOS using AppleScript.

## Capabilities

- **Pane Management**: Split panes vertically/horizontally
- **Tab Management**: Create, close, navigate, rename tabs
- **Window Management**: Create windows, apply profiles
- **Profile Switching**: Apply different terminal profiles
- **Color Themes**: Quick dark/light mode switching, custom colors
- **Broadcast Input**: Send keystrokes to multiple panes
- **Layouts**: Create development workspace layouts
- **Command Dispatch**: Send commands to specific panes

## Quick Reference

| Command | Purpose | Example |
|---------|---------|---------|
| `/iterm:pane` | Split current pane | `/iterm:pane h` (horizontal) |
| `/iterm:tab` | Manage tabs | `/iterm:tab new`, `/iterm:tab rename Server` |
| `/iterm:window` | Manage windows | `/iterm:window new`, `/iterm:window profile Dev` |
| `/iterm:profile` | Switch profiles | `/iterm:profile Hotkey` |
| `/iterm:theme` | Change colors | `/iterm:theme dark`, `/iterm:theme bg 1a1a2e` |
| `/iterm:broadcast` | Toggle broadcast | `/iterm:broadcast on` |
| `/iterm:layout` | Apply layouts | `/iterm:layout grid`, `/iterm:layout dev` |
| `/iterm:send` | Send commands | `/iterm:send npm start` |

## Common Workflows

### Multi-Service Development

Set up a development environment with multiple services:

1. `/iterm:layout dev` - Create development layout (main + logs + terminal)
2. `/iterm:send --all cd ~/project` - Navigate all panes to project
3. Start different services in each pane:
   - Main pane: code editor or main service
   - Logs pane: `tail -f logs/app.log`
   - Terminal pane: running commands

### Server Monitoring

Monitor multiple servers simultaneously:

1. `/iterm:layout grid` - Create 4-pane grid
2. SSH to different servers in each pane
3. `/iterm:broadcast on` - Enable synchronized input
4. Run same commands on all servers at once

### Quick Theme Switching

Switch between light and dark modes:

- `/iterm:theme dark` - For low-light environments
- `/iterm:theme light` - For bright environments
- `/iterm:theme bg 1a1a2e` - Custom dark blue background

## AppleScript Basics

All commands use `osascript` to execute AppleScript. The basic pattern:

```applescript
tell application "iTerm2"
  tell current session of current tab of current window
    -- Action here
  end tell
end tell
```

### Object Hierarchy

```
iTerm2 (Application)
└── Window
    └── Tab
        └── Session (Pane)
```

### Common Operations

```applescript
-- Split pane
split vertically with default profile
split horizontally with default profile

-- Write command
write text "your command"

-- Set colors (values 0-65535)
set background color to {R, G, B, 65535}
set foreground color to {R, G, B, 65535}

-- Create tab/window
tell current window to create tab with default profile
create window with profile "ProfileName"
```

## Requirements

- **Platform**: macOS only
- **Dependencies**: iTerm2 must be installed and running
- **Permissions**: AppleScript automation permissions required

## Troubleshooting

### "Not authorized to send Apple events"

Grant automation permissions:
1. Open System Preferences > Privacy & Security > Privacy
2. Select "Automation" in the sidebar
3. Find your terminal app (Terminal or iTerm2)
4. Enable access to "iTerm2"

### "iTerm2 is not running"

All commands require iTerm2 to be open. Start iTerm2 first, then run commands.

### Broadcast not working

Broadcast requires System Events permissions:
1. Open System Preferences > Privacy & Security > Privacy
2. Select "Accessibility" in the sidebar
3. Add your terminal app

## Further Reading

- [Installation Guide](guides/installation.md)
- [AppleScript Reference](guides/applescript.md)
- [Workflow Patterns](guides/workflows.md)
