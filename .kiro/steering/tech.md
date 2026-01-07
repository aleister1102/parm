# Parm - Tech Stack

## Language & Runtime

- Go 1.24+
- Module name: `parm`

## Key Dependencies

- `github.com/spf13/cobra` - CLI framework
- `github.com/spf13/viper` - Configuration management
- `github.com/google/go-github/v74` - GitHub API client
- `github.com/Masterminds/semver/v3` - Semantic versioning
- `github.com/vbauerster/mpb/v8` - Progress bars
- `github.com/h2non/filetype` - File type detection
- `github.com/shirou/gopsutil/v4` - System/process utilities
- `golang.org/x/oauth2` - OAuth2 for GitHub authentication

## Testing

- `github.com/migueleliasweb/go-github-mock` - GitHub API mocking

## Build System

Uses Make with the following targets:

```bash
make build      # Build binary for current platform → bin/parm
make test       # Run all tests
make install    # Build and install to ~/.local/bin
make uninstall  # Remove from ~/.local/bin
make clean      # Remove build artifacts

# Release targets
make release TAG=v1.0.0  # Create GitHub release with cross-platform binaries
make bump-patch          # Release next patch version
make bump-minor          # Release next minor version
make bump-major          # Release next major version
```

## Version Injection

Version is injected at build time via ldflags:
```
-X 'parm/parmver.StringVersion=$(TAG)'
```

## Linting

Uses golangci-lint with `errcheck` disabled (see `.golangci.yaml`).

## Cross-Platform Builds

Release builds target:
- linux/amd64, linux/arm64
- darwin/amd64, darwin/arm64
- windows/amd64, windows/arm64
