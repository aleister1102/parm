# Parm - Product Overview

Parm is a cross-platform CLI binary installer that downloads and manages programs directly from GitHub releases.

## Key Characteristics

- Zero root access required
- Zero external dependencies
- Downloads prebuilt binaries from GitHub release assets
- Symlinks binaries to PATH for easy access
- Supports version pinning and update checking
- Works on Linux, macOS, and Windows

## Core Functionality

- `install <owner>/<repo>` - Install packages from GitHub releases
- `remove <owner>/<repo>` - Uninstall packages
- `update <owner>/<repo>` - Update installed packages
- `list` - Show installed packages
- `info` - Get package information
- `config` - Manage configuration settings

## Design Philosophy

Parm complements (not replaces) system package managers. It's designed for high-level, user-facing applications distributed via GitHub releases, not low-level system libraries.

## Limitations

- Does not automatically resolve/install dependencies
- Uses GitHub API (rate-limited without token: 60 req/hr, with token: 5000+ req/hr)
- Users are responsible for vetting packages they install
