# itmux Starter Guide

A beginner-friendly guide to getting started with itmux - Tmux for Windows.

## Table of Contents

1. [What is itmux?](#what-is-itmux)
2. [Installation](#installation)
3. [Getting Started](#getting-started)
4. [Essential Keybindings](#essential-keybindings)
5. [Working with Windows](#working-with-windows)
6. [Working with Panes](#working-with-panes)
7. [Session Management](#session-management)
8. [Configuration](#configuration)
9. [Tips and Tricks](#tips-and-tricks)
10. [Additional Resources](#additional-resources)

---

## What is itmux?

itmux packages Tmux, Mintty, OpenSSH client, and Cygwin into a standalone terminal multiplexer for Windows. Tmux allows you to:

- **Run multiple programs** from a single terminal window
- **Detach and reattach** to sessions without losing your work
- **Split your screen** into multiple panes for simultaneous tasks
- **Manage multiple windows** within a single session
- **Protect your work** from accidental disconnections

This is especially useful for:
- Remote SSH connections that need to persist
- Running long-running processes
- Managing multiple command-line tasks simultaneously
- Organizing your workspace efficiently

---

## Installation

1. Download the latest itmux release from [GitHub Releases](https://github.com/itefixnet/itmux/releases)
2. Extract the ZIP archive to your desired location
3. No installation required - itmux is fully portable!

---

## Getting Started

### Launching itmux

1. Navigate to the extracted itmux directory
2. Double-click `tmux.cmd` to launch the Mintty terminal
3. Type `tmux` and press Enter to start your first session

```bash
tmux
```

You should see a green status bar at the bottom of your terminal - you're now in a tmux session!

### Understanding the Interface

The tmux interface consists of:
- **Status bar** (bottom): Shows session name, windows, and system information
- **Window**: The full terminal view (like a tab in a browser)
- **Pane**: A split section within a window

---

## Essential Keybindings

All tmux commands start with a **prefix key**. By default, this is `Ctrl+B`. Here's how it works:

1. Press `Ctrl+B`
2. Release both keys
3. Press the command key

We'll write this as `Ctrl+B` then `key` throughout this guide.

> **💡 Tip:** Many users find `Ctrl+B` awkward to press with one hand. The configuration section below shows how to change it to `Ctrl+A`, which is more comfortable and easier to reach.

### Most Important Commands

| Command | Action |
|---------|--------|
| `Ctrl+B` then `?` | Show all keybindings (press `Q` to exit) |
| `Ctrl+B` then `D` | Detach from session |
| `Ctrl+B` then `:` | Enter command mode |
| `Ctrl+B` then `[` | Enter scroll mode (use arrow keys, press `Q` to exit) |

---

## Working with Windows

Think of windows like tabs in a web browser - each window is a separate terminal view.

### Window Commands

| Command | Action |
|---------|--------|
| `Ctrl+B` then `C` | Create new window |
| `Ctrl+B` then `N` | Next window |
| `Ctrl+B` then `P` | Previous window |
| `Ctrl+B` then `0-9` | Switch to window by number |
| `Ctrl+B` then `,` | Rename current window |
| `Ctrl+B` then `W` | List all windows (navigate with arrows) |
| `Ctrl+B` then `&` | Kill current window (with confirmation) |

### Example: Multi-Window Workflow

```bash
# Start tmux
tmux

# Create a window for logs
Ctrl+B then C
tail -f application.log

# Create a window for editing
Ctrl+B then C
vim config.txt

# Create a window for running tests
Ctrl+B then C
./run-tests.sh

# Switch between windows
Ctrl+B then 0  # Go to first window
Ctrl+B then 1  # Go to second window
Ctrl+B then N  # Next window
```

---

## Working with Panes

Panes let you split a single window into multiple sections, each running its own terminal.

### Pane Commands

| Command | Action |
|---------|--------|
| `Ctrl+B` then `%` | Split pane vertically (left/right) |
| `Ctrl+B` then `"` | Split pane horizontally (top/bottom) |
| `Ctrl+B` then `Arrow Key` | Move between panes |
| `Ctrl+B` then `O` | Cycle through panes |
| `Ctrl+B` then `X` | Kill current pane (with confirmation) |
| `Ctrl+B` then `Z` | Toggle pane zoom (fullscreen) |
| `Ctrl+B` then `Space` | Cycle through pane layouts |
| `Ctrl+B` then `{` | Move current pane left |
| `Ctrl+B` then `}` | Move current pane right |

### Resizing Panes

Hold `Ctrl+B` and use arrow keys while holding `Ctrl`:

```
Ctrl+B then Ctrl+Arrow Key  # Resize in arrow direction
```

### Example: Split Screen Workflow

```bash
# Start with one pane
tmux

# Split horizontally (top/bottom)
Ctrl+B then "

# In bottom pane, run a server
npm start

# Move to top pane
Ctrl+B then Up Arrow

# Split top pane vertically (left/right)
Ctrl+B then %

# Now you have 3 panes: top-left, top-right, and bottom
# Navigate between them with Ctrl+B then Arrow Keys
```

---

## Session Management

Sessions are tmux's killer feature - they let you detach and reattach to running terminals.

### Creating Sessions

```bash
# Start new session with a name
tmux new -s myproject

# Or simply
tmux new-session -s myproject
```

### Detaching and Attaching

```bash
# Detach from current session
Ctrl+B then D

# List all sessions
tmux ls
# or
tmux list-sessions

# Attach to a session
tmux attach -t myproject
# or
tmux a -t myproject

# Attach to last session
tmux attach
```

### Managing Sessions

```bash
# Kill a session
tmux kill-session -t myproject

# Kill all sessions except current
tmux kill-session -a

# Rename current session
Ctrl+B then $
```

### Real-World Example: Persistent Development Environment

```bash
# Morning: Start your dev session
tmux new -s dev

# Create windows for different tasks
Ctrl+B then C  # Window 1: Editor
Ctrl+B then ,  # Rename to "editor"
vim main.py

Ctrl+B then C  # Window 2: Server
Ctrl+B then ,  # Rename to "server"
python app.py

Ctrl+B then C  # Window 3: Tests
Ctrl+B then ,  # Rename to "tests"
pytest --watch

# Lunch time: Detach
Ctrl+B then D

# Afternoon: Resume exactly where you left off
tmux attach -t dev

# End of day: Keep it running for tomorrow
Ctrl+B then D
```

---

## Configuration

### Enabling Mouse Support

To use your mouse in tmux:

```bash
# Enter command mode
Ctrl+B then :

# Enable mouse
set -g mouse on
```

Now you can:
- Click to switch panes
- Click window names in status bar
- Right-click for context menu
- Drag pane borders to resize
- Scroll with mouse wheel

### Permanent Configuration

Create a configuration file to customize tmux:

```bash
# In your home directory, create .tmux.conf
vim ~/.tmux.conf
```

#### Recommended Best Practices Configuration

Here's a well-optimized configuration that includes essential improvements and best practices:

```bash
# =====================================
# PREFIX KEY - More Comfortable
# =====================================
# Change prefix from Ctrl+B to Ctrl+A
# Ctrl+A is easier to press with one hand
set -g prefix C-a
unbind C-b
bind C-a send-prefix

# =====================================
# MOUSE SUPPORT - Modern Convenience
# =====================================
# Enable mouse for easier window/pane management
set -g mouse on

# =====================================
# INDEXING - More Intuitive
# =====================================
# Start windows and panes at 1, not 0
# Matches keyboard number row layout
set -g base-index 1
setw -g pane-base-index 1

# Renumber windows when one is closed
set -g renumber-windows on

# =====================================
# SCROLLBACK - More History
# =====================================
# Increase scrollback buffer from 2000 to 50000
set -g history-limit 50000

# =====================================
# DISPLAY - Better Timing
# =====================================
# Display messages for 4 seconds
set -g display-time 4000

# Increase display time for pane numbers
set -g display-panes-time 3000

# =====================================
# RESPONSIVENESS - Faster Commands
# =====================================
# Reduce escape time for faster command sequences
# Especially important for vim users
set -sg escape-time 0

# Allow faster key repetition
set -g repeat-time 600

# =====================================
# FOCUS EVENTS - Better App Integration
# =====================================
# Enable focus events for better editor integration
set -g focus-events on

# =====================================
# COLORS - True Color Support
# =====================================
# Enable 256 colors
set -g default-terminal "screen-256color"

# Enable true color support (if terminal supports it)
set -ga terminal-overrides ",*256col*:Tc"

# =====================================
# STATUS BAR - Better Visibility
# =====================================
# Status bar colors (more readable than default green)
set -g status-style bg=colour234,fg=colour137

# Current window highlighting
set -g window-status-current-style bg=colour238,fg=colour81,bold

# Inactive window style
set -g window-status-style fg=colour138,bg=colour235,none

# Pane border colors
set -g pane-border-style fg=colour238
set -g pane-active-border-style fg=colour81

# Message style
set -g message-style bg=colour235,fg=colour81

# Status bar format
set -g status-left-length 20
set -g status-left '#[fg=colour81,bold] #S #[default]'
set -g status-right '#[fg=colour233,bg=colour241,bold] %m/%d #[fg=colour233,bg=colour245,bold] %H:%M '

# =====================================
# WINDOW/PANE SPLITTING - More Intuitive
# =====================================
# Split panes using | and - (more intuitive than % and ")
bind | split-window -h -c "#{pane_current_path}"
bind - split-window -v -c "#{pane_current_path}"
unbind '"'
unbind %

# New windows open in current path
bind c new-window -c "#{pane_current_path}"

# =====================================
# PANE NAVIGATION - Vim-style
# =====================================
# Switch panes using Alt+arrow without prefix
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

# Vim-style pane navigation (optional, uncomment if you prefer)
# bind h select-pane -L
# bind j select-pane -D
# bind k select-pane -U
# bind l select-pane -R

# =====================================
# PANE RESIZING - Easier Control
# =====================================
# Resize panes more easily
bind -r H resize-pane -L 5
bind -r J resize-pane -D 5
bind -r K resize-pane -U 5
bind -r L resize-pane -R 5

# =====================================
# COPY MODE - Vi-style
# =====================================
# Use vi keys in copy mode
setw -g mode-keys vi

# Better copy mode bindings (vi-style)
bind -T copy-mode-vi v send -X begin-selection
bind -T copy-mode-vi y send -X copy-selection-and-cancel
bind -T copy-mode-vi C-v send -X rectangle-toggle

# =====================================
# RELOAD CONFIG - Quick Access
# =====================================
# Reload config file with prefix+r
bind r source-file ~/.tmux.conf \; display "Config reloaded!"

# =====================================
# SESSION MANAGEMENT - Easier Switching
# =====================================
# Quick session switching
bind -n C-M-j switch-client -n
bind -n C-M-k switch-client -p

# =====================================
# ACTIVITY MONITORING
# =====================================
# Highlight window with activity
setw -g monitor-activity on
set -g visual-activity off

# =====================================
# CLIPBOARD INTEGRATION (Windows/Cygwin)
# =====================================
# Copy to Windows clipboard (requires /dev/clipboard in Cygwin)
bind -T copy-mode-vi y send-keys -X copy-pipe-and-cancel "cat > /dev/clipboard"

# =====================================
# MISC IMPROVEMENTS
# =====================================
# Don't rename windows automatically
set -g allow-rename off

# Aggressive resize (useful for multi-monitor setups)
setw -g aggressive-resize on
```

#### Quick Configuration Options

If you prefer a minimal configuration, here are the most important settings:

```bash
# Minimal but powerful configuration
set -g prefix C-a              # Better prefix key
unbind C-b
bind C-a send-prefix
set -g mouse on                # Enable mouse
set -g base-index 1            # Start at 1, not 0
setw -g pane-base-index 1
set -g history-limit 50000     # More history
set -sg escape-time 0          # Faster commands
bind r source-file ~/.tmux.conf \; display "Reloaded!"
bind | split-window -h         # Intuitive split
bind - split-window -v
```

After saving, reload the configuration:

```bash
Ctrl+B then :
source-file ~/.tmux.conf
```

Or use the custom keybinding:

```bash
Ctrl+B then R
```

---

## Tips and Tricks

### Quick Reference Commands

```bash
# List all commands
tmux list-commands

# List all keybindings
Ctrl+B then ?

# Show message in status bar
Ctrl+B then :
display-message "Hello tmux!"
```

### Command Mode Tips

Enter command mode with `Ctrl+B` then `:` for direct commands:

```bash
# Create new window with name
new-window -n "logs"

# Split pane with specific size
split-window -h -p 30  # 30% width

# Kill all windows except current
kill-window -a
```

### Synchronize Panes

Run the same command in all panes simultaneously:

```bash
Ctrl+B then :
setw synchronize-panes on

# Now typing in one pane types in all panes
# Useful for managing multiple servers

# Turn off synchronization
Ctrl+B then :
setw synchronize-panes off
```

### Copy Mode (Scrolling and Copying Text)

```bash
# Enter copy mode
Ctrl+B then [

# Navigate with:
# - Arrow keys
# - Page Up/Down
# - Search with / (forward) or ? (backward)

# Start selection (vi mode)
Space

# Copy selection (vi mode)
Enter

# Paste
Ctrl+B then ]

# Exit copy mode
Q
```

### View Pane Numbers

```bash
# Display pane numbers
Ctrl+B then Q

# Switch to pane by number
Ctrl+B then Q then [number]
```

---

## Additional Resources

### Learning More

- **[A Beginner's Guide to Tmux](https://www.redhat.com/en/blog/introduction-tmux-linux)** - Comprehensive tutorial from Red Hat
- **[Tmux Cheat Sheet](https://opensource.com/downloads/tmux-cheat-sheet)** - Quick reference PDF
- **[Official Tmux Wiki](https://github.com/tmux/tmux/wiki)** - Complete documentation

### Common Use Cases

#### 1. Remote Server Management

```bash
# Connect to server
ssh user@server

# Start named tmux session
tmux new -s server-work

# Do your work...
# If connection drops, tmux keeps running!

# Reconnect to server
ssh user@server

# Reattach to session
tmux attach -t server-work
```

#### 2. Long-Running Processes

```bash
# Start tmux
tmux new -s build

# Run long build
./build-script.sh

# Detach with Ctrl+B then D
# Close terminal window
# Come back hours later
tmux attach -t build
# Your build is still running!
```

#### 3. Project Workspace

```bash
# Create project session
tmux new -s myapp

# Window 0: Code
vim src/

# Window 1: Server
Ctrl+B then C
npm run dev

# Window 2: Database
Ctrl+B then C
mongod

# Window 3: Tests
Ctrl+B then C
npm test -- --watch

# Save this setup as a script!
```

### Creating Startup Scripts

Create a script to launch your perfect workspace:

```bash
#!/bin/bash
# start-dev.sh

# Create session
tmux new-session -d -s dev

# Window 0: Editor
tmux rename-window -t dev:0 'editor'
tmux send-keys -t dev:0 'cd ~/projects/myapp && vim' C-m

# Window 1: Server
tmux new-window -t dev:1 -n 'server'
tmux send-keys -t dev:1 'cd ~/projects/myapp && npm start' C-m

# Window 2: Tests
tmux new-window -t dev:2 -n 'tests'
tmux send-keys -t dev:2 'cd ~/projects/myapp && npm test' C-m

# Attach to session
tmux attach-session -t dev
```

Run with: `./start-dev.sh`

---

## Getting Help

- **Within tmux**: Press `Ctrl+B` then `?` to see all keybindings
- **Command help**: `tmux list-commands` or `man tmux` (in Unix environments)
- **GitHub Issues**: https://github.com/itefixnet/itmux/issues
- **itmux Homepage**: https://itefix.net/itmux

---

## Quick Start Checklist

- [ ] Download and extract itmux
- [ ] Launch `tmux.cmd` and run `tmux`
- [ ] Try creating a new window (`Ctrl+B` then `C`)
- [ ] Try splitting panes (`Ctrl+B` then `"` or `%`)
- [ ] Practice detaching (`Ctrl+B` then `D`) and reattaching (`tmux attach`)
- [ ] Enable mouse support (`Ctrl+B` then `:` → `set -g mouse on`)
- [ ] Create your `.tmux.conf` file
- [ ] Learn the most important commands (see Essential Keybindings)

Welcome to the world of tmux! With practice, these commands will become second nature, and you'll wonder how you ever managed without a terminal multiplexer.
