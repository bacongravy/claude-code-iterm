# Installation Guide

## Prerequisites

- **macOS**: This plugin only works on macOS
- **iTerm2**: Download from [iterm2.com](https://iterm2.com) if not installed
- **Claude Code**: The Claude Code CLI must be installed

## Installation

### Option 1: Local Plugin Directory

For development or personal use:

```bash
claude --plugin-dir /path/to/claude-code-iterm
```

### Option 2: Install from Path

Install the plugin to your Claude Code configuration:

```bash
/plugin install /path/to/claude-code-iterm
```

### Option 3: From Git Repository

Clone and install:

```bash
git clone https://github.com/yourusername/claude-code-iterm.git
/plugin install /path/to/claude-code-iterm
```

## Granting Permissions

### AppleScript Automation

When you first use the plugin, macOS will prompt for automation permissions:

1. A dialog will appear: "Terminal wants to control iTerm2"
2. Click "OK" to allow

If you accidentally denied permission:

1. Open **System Preferences** > **Privacy & Security** > **Privacy**
2. Select **Automation** in the sidebar
3. Find your terminal app
4. Check the box next to **iTerm2**

### Accessibility (for Broadcast)

The broadcast command uses keyboard simulation which requires accessibility permissions:

1. Open **System Preferences** > **Privacy & Security** > **Privacy**
2. Select **Accessibility** in the sidebar
3. Click the lock icon to make changes
4. Add your terminal app (Terminal, iTerm2, or whichever you use with Claude Code)

## Verifying Installation

Test that the plugin is working:

```bash
# In Claude Code, run:
/iterm:pane
```

This should split your current iTerm2 pane vertically.

## Uninstallation

Remove the plugin:

```bash
/plugin uninstall iterm
```

Or if using the `--plugin-dir` flag, simply stop using that flag.

## Troubleshooting

### "Plugin not found"

Ensure the path to the plugin directory is correct. The directory should contain:
- `.claude-plugin/plugin.json`
- `commands/` directory

### "iTerm2 is not running"

The plugin requires iTerm2 to be open. Start iTerm2 before running commands.

### Commands silently fail

Check that:
1. iTerm2 is the active terminal application
2. Automation permissions are granted
3. You're running on macOS (not Linux/Windows)
