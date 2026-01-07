# Parm - Project Structure

```
parm/
├── main.go                 # Entry point
├── parmver/                # Version info (injected at build)
├── cmd/                    # CLI commands (Cobra)
│   ├── root.go             # Root command, wires subcommands
│   ├── install/            # install command
│   ├── remove/             # remove command
│   ├── update/             # update command
│   ├── list/               # list command
│   ├── info/               # info command
│   ├── search/             # search command
│   ├── pin/                # pin/unpin commands
│   ├── sw/                 # switch channel command
│   └── configure/          # config commands (set, reset)
├── internal/               # Private application code
│   ├── cmdutil/            # Command utilities (Factory pattern)
│   ├── config/             # Configuration loading/management
│   ├── gh/                 # GitHub API client wrapper
│   ├── manifest/           # Package manifest handling
│   ├── parmutil/           # Parm-specific utilities
│   └── core/               # Core business logic
│       ├── catalog/        # Package catalog operations
│       ├── installer/      # Installation logic
│       ├── uninstaller/    # Uninstallation logic
│       ├── updater/        # Update/pin logic
│       ├── switcher/       # Channel switching
│       └── verify/         # Integrity verification
├── pkg/                    # Reusable packages
│   ├── archive/            # Archive extraction (tar, zip)
│   ├── cmdparser/          # Command argument parsing
│   ├── cmdx/               # Cobra command extensions
│   ├── deps/               # Dependency detection
│   ├── progress/           # Progress bar hooks
│   └── sysutil/            # System utilities (files, links, processes)
├── scripts/                # Build/release scripts
└── docs/                   # Documentation
```

## Architecture Patterns

### Factory Pattern
Commands receive a `*cmdutil.Factory` for dependency injection, enabling testable GitHub client creation.

### Command Structure
Each command lives in its own package under `cmd/` with a `New<Command>Cmd(f *Factory) *cobra.Command` constructor.

### Internal vs Pkg
- `internal/` - Application-specific code, not importable externally
- `pkg/` - Generic, reusable utilities that could be imported by other projects

### Core Modules
Business logic in `internal/core/` is separated by domain (installer, updater, etc.), each with its own package.

### Configuration
- Uses Viper for config management
- Config file: `$XDG_CONFIG_HOME/parm/config.toml`
- Supports env vars: `PARM_GITHUB_TOKEN`, `GITHUB_TOKEN`, `GH_TOKEN`

### Data Storage
- Linux: `~/.local/share/parm/`
- macOS: `~/Library/Application Support/parm/`
- Windows: `~/.parm/`
