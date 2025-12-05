# itmux - Tmux for Windows

![itmux](tmux.png)

itmux is a packaging of Tmux, Mintty, OpenSSH client and Cygwin to offer a standalone ssh-enabled terminal multiplexer for Windows systems.

[tmux](https://github.com/tmux/tmux/wiki) (Terminal Multiplexer) is a popular command-line tool that allows users to manage multiple terminal sessions from a single window, making it easier to work with multiple command-line tasks simultaneously. Originally created as an open-source alternative to GNU Screen, tmux has become widely used among developers, system administrators, and anyone who works extensively in the command line.

## Features

- **Terminal multiplexer**: Manage multiple terminal sessions from a single window
- **Mintty terminal**: Lightweight, efficient terminal emulator with Unix-like interface
- **OpenSSH client**: Secure remote access and file transfer capabilities
- **Cygwin environment**: Linux-like environment for Windows with substantial Linux API functionality
- **Portable**: Unzip and run, no installation or system modifications required
- **Session management**: Create, detach, and reattach terminal sessions
- **Window splitting**: Split terminal into multiple panes for simultaneous tasks
- **Wide compatibility**: Works on modern Windows systems

## Requirements

- Windows operating system
- No external dependencies required — all components included in the package

## Download

Latest releases of itmux are available on GitHub:

https://github.com/itefixnet/itmux/releases

Each release includes:
- The complete itmux ZIP package (Tmux, Mintty, OpenSSH client, Cygwin runtime)
- Release notes and version history

## Basic Usage

1. Unzip the downloaded archive

2. Start tmux.cmd at the root directory to initiate a mintty terminal

3. Start tmux:
   ```
   tmux
   ```

### Getting Started with Tmux

For those new to tmux, check out our comprehensive starter guide:

- **[itmux Starter Guide](STARTER_GUIDE.md)** - Complete beginner-friendly guide with examples and best practices

Additional external resources:

- [A beginner's guide to tmux](https://www.redhat.com/en/blog/introduction-tmux-linux)
- [Tmux cheat sheet](https://opensource.com/downloads/tmux-cheat-sheet)

itmux is tested successfully with various workflows. You should test and verify that it works for your specific needs.

## Links

- **Tmux homepage**: https://github.com/tmux/tmux/wiki
- **Mintty homepage**: https://mintty.github.io/
- **OpenSSH homepage**: https://www.openssh.com/
- **Cygwin homepage**: http://www.cygwin.com/

## License

itmux is licensed under the BSD 2-Clause License. See LICENSE file for details.
