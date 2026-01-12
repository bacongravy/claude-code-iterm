# Claude Code iTerm2 Plugin

A Claude Code plugin for automating iTerm2 terminal operations on macOS.

## Features

- **Pane Management** - Split panes vertically and horizontally
- **Tab Management** - Create, close, navigate, and rename tabs
- **Window Management** - Create windows with specific profiles
- **Profile Switching** - Apply different iTerm2 profiles
- **Color Themes** - Quick dark/light mode and custom color switching
- **Broadcast Input** - Send keystrokes to multiple panes simultaneously
- **Preset Layouts** - Create development workspace layouts (grid, sidebar, dev)
- **Command Dispatch** - Send commands to specific panes

## Installation

### From Marketplace (Recommended)

```bash
/plugin marketplace add https://github.com/bacongravy/claude-code-marketplace
/plugin install iterm@bacongravy
```

### From Repository

```bash
/plugin install https://github.com/bacongravy/claude-code-iterm
```

### For Development

```bash
claude --plugin-dir /path/to/claude-code-iterm
```

## Commands

### `/iterm:pane` - Split Panes

Split the current pane vertically or horizontally.

```bash
/iterm:pane           # Split vertically (new pane to the right)
/iterm:pane h         # Split horizontally (new pane below)
/iterm:pane v         # Explicit vertical split
/iterm:pane horizontal
/iterm:pane vertical
```

### `/iterm:tab` - Manage Tabs

Create, close, navigate, and rename tabs.

```bash
/iterm:tab new        # Create new tab
/iterm:tab close      # Close current tab
/iterm:tab next       # Switch to next tab
/iterm:tab prev       # Switch to previous tab
/iterm:tab goto 3     # Go to tab 3
/iterm:tab rename API # Rename current tab to "API"
```

### `/iterm:window` - Manage Windows

Create and manage windows.

```bash
/iterm:window new           # Create new window with default profile
/iterm:window close         # Close current window
/iterm:window profile Dev   # Create window with "Dev" profile
```

### `/iterm:profile` - Switch Profiles

Apply a different iTerm2 profile to the current session.

```bash
/iterm:profile Default      # Switch to Default profile
/iterm:profile "Hotkey Window"
```

### `/iterm:theme` - Change Colors

Quickly change terminal colors.

```bash
/iterm:theme dark           # Dark theme (black bg, white text)
/iterm:theme light          # Light theme (white bg, black text)
/iterm:theme bg 1a1a2e      # Set background to hex color
/iterm:theme fg 00ff00      # Set foreground to hex color
```

### `/iterm:broadcast` - Broadcast Input

Toggle broadcast mode to send keystrokes to multiple panes.

```bash
/iterm:broadcast on         # Enable broadcast
/iterm:broadcast off        # Disable broadcast
/iterm:broadcast toggle     # Toggle broadcast
/iterm:broadcast            # Toggle (default)
```

### `/iterm:layout` - Preset Layouts

Create common pane layouts.

```bash
/iterm:layout grid          # 2x2 grid (4 panes)
/iterm:layout sidebar       # Main pane + narrow sidebar
/iterm:layout stack         # Main pane + 2 panes below
/iterm:layout dev           # Development layout (main + logs + terminal)
```

**Layout diagrams:**

```
grid:           sidebar:        stack:          dev:
┌────┬────┐     ┌──────┬──┐     ┌──────────┐     ┌──────┬──┐
│  1 │  2 │     │      │  │     │   Main   │     │      │  │
├────┼────┤     │ Main │S │     ├────┬─────┤     │ Main │L │
│  3 │  4 │     │      │  │     │  2 │  3  │     ├──────┴──┤
└────┴────┘     └──────┴──┘     └────┴─────┘     │ Terminal│
                                                 └─────────┘
```

### `/iterm:send` - Send Commands

Send a command to panes.

```bash
/iterm:send npm start           # Send to current pane
/iterm:send --all clear         # Send to all panes in tab
/iterm:send --all cd ~/project  # Navigate all panes
```

## Requirements

- macOS
- iTerm2 installed and running
- Claude Code CLI
- AppleScript automation permissions

## Permissions

On first use, macOS will prompt for permissions:

1. **Automation**: Allow your terminal to control iTerm2
2. **Accessibility**: Required for broadcast feature (keyboard simulation)

Grant permissions in **System Preferences** > **Privacy & Security** > **Privacy**.

## Examples

### Development Workflow

```bash
# Set up development environment
/iterm:layout dev
/iterm:send --all cd ~/myproject
# Main: start dev server
# Logs: tail -f logs/app.log
# Terminal: run commands
```

### Multi-Server Administration

```bash
# Create grid for 4 servers
/iterm:layout grid
# SSH to servers in each pane...
/iterm:broadcast on
# Commands now go to all servers
sudo systemctl status nginx
```

### Quick Theme Toggle

```bash
/iterm:theme dark    # Night mode
/iterm:theme light   # Day mode
```

## Troubleshooting

### "Not authorized to send Apple events"

1. Open System Preferences > Privacy & Security > Privacy
2. Select Automation
3. Enable iTerm2 access for your terminal

### Commands silently fail

- Ensure iTerm2 is running
- Check you're on macOS
- Verify automation permissions

### Broadcast not working

- Grant Accessibility permissions
- iTerm2 must be the frontmost application

## Documentation

- [Installation Guide](skills/iterm/guides/installation.md)
- [AppleScript Reference](skills/iterm/guides/applescript.md)
- [Workflow Patterns](skills/iterm/guides/workflows.md)

## License

MIT
