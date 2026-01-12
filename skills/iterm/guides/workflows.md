# Common Workflow Patterns

This guide provides workflow patterns for using the iTerm2 plugin in development scenarios.

## Development Environment Setup

### Full-Stack Development

Create a layout for working on a full-stack application:

```bash
# Create the dev layout (main + logs + terminal)
/iterm:layout dev

# In the main pane: start your development server
# In the logs pane: tail your log files
# In the terminal pane: run commands
```

Manual equivalent:
1. `/iterm:pane h` - Split horizontally (terminal below)
2. Navigate to top pane
3. `/iterm:pane` - Split vertically (logs sidebar)

### Microservices Development

Set up a grid for multiple services:

```bash
# Create 4-pane grid
/iterm:layout grid

# Navigate all panes to project root
/iterm:send --all cd ~/projects/myapp

# Start different services in each pane
# Pane 1: Frontend - npm run dev
# Pane 2: API - npm run api
# Pane 3: Database - docker-compose up db
# Pane 4: Logs - tail -f logs/*.log
```

### Quick Service + Logs

Simple two-pane setup for a service and its logs:

```bash
# Split pane and set up
/iterm:pane
# Left pane: run service
# Right pane: tail logs
```

## Server Administration

### Multi-Server Management

Manage multiple servers simultaneously:

```bash
# Create grid for 4 servers
/iterm:layout grid

# SSH to each server (manually in each pane)
# server1.example.com
# server2.example.com
# server3.example.com
# server4.example.com

# Enable broadcast to run same commands everywhere
/iterm:broadcast on

# Now commands go to all servers:
# sudo apt update
# sudo systemctl status nginx
```

### Staged Deployment

Set up panes for staging and production:

```bash
# Create sidebar layout (main + side)
/iterm:layout sidebar

# Left pane: staging server
# Right pane: production server

# Deploy to staging first, verify, then production
```

## Log Monitoring

### Multi-Log Monitoring

Watch multiple log files simultaneously:

```bash
# Create grid
/iterm:layout grid

# In each pane, tail a different log:
# tail -f /var/log/nginx/access.log
# tail -f /var/log/nginx/error.log
# tail -f /var/log/app/app.log
# tail -f /var/log/syslog
```

### Development Logs

Monitor development logs with dark theme:

```bash
# Set dark theme for better log visibility
/iterm:theme dark

# Split for logs
/iterm:pane

# Left: development server
# Right: tail -f logs/development.log
```

## Git Workflows

### Code Review Setup

Set up panes for reviewing code:

```bash
# Create sidebar layout
/iterm:layout sidebar

# Main pane: browse code / editor
# Sidebar: git log --oneline --graph
#          or git diff
```

### Multi-Repo Management

Manage multiple repositories:

```bash
# Create grid
/iterm:layout grid

# Navigate each pane to different repos
# Then sync all with broadcast:
/iterm:broadcast on
# git pull
# git status
```

## Testing Workflows

### Test + Code Setup

```bash
# Split vertically
/iterm:pane

# Left pane: editor / code
# Right pane: npm test --watch
```

### Integration Testing

```bash
# Create stack layout (main + 2 below)
/iterm:layout stack

# Main: application
# Bottom left: database
# Bottom right: test runner
```

## Quick Toggles

### Dark Mode for Night Work

```bash
/iterm:theme dark
# Work in low light...
/iterm:theme light
```

### Custom Brand Colors

```bash
# Company blue background
/iterm:theme bg 0066cc

# Matrix green on black
/iterm:theme bg 000000
/iterm:theme fg 00ff00
```

## Tab Organization

### Project-Per-Tab

```bash
# Tab 1: Frontend
/iterm:tab rename Frontend
/iterm:send cd ~/projects/frontend

# Create new tab for backend
/iterm:tab new
/iterm:tab rename Backend
/iterm:send cd ~/projects/backend

# Switch between projects
/iterm:tab goto 1  # Frontend
/iterm:tab goto 2  # Backend
```

### Environment-Per-Tab

```bash
# Tab 1: Development
/iterm:tab rename Dev

# Tab 2: Staging
/iterm:tab new
/iterm:tab rename Staging

# Tab 3: Production
/iterm:tab new
/iterm:tab rename Prod
```

## Combining Commands

### Quick Development Start

Typical morning routine:

```bash
# Create dev layout
/iterm:layout dev

# Navigate to project
/iterm:send --all cd ~/myproject

# Start services (manually in each pane):
# Main: code .
# Logs: npm run logs
# Terminal: ready for commands
```

### Server Maintenance Session

```bash
# New window for maintenance
/iterm:window profile Maintenance

# Create grid for multiple servers
/iterm:layout grid

# Connect to servers and enable broadcast
# ... SSH connections ...
/iterm:broadcast on
```

## Best Practices

1. **Name your tabs** - Use `/iterm:tab rename` to keep tabs organized
2. **Use layouts** - Start with a layout rather than manual splitting
3. **Broadcast carefully** - Always verify you're in the right panes before enabling broadcast
4. **Dark theme for logs** - Dark backgrounds make log output easier to read
5. **Project-per-window** - Use separate windows for unrelated projects
