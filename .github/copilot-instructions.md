<!-- file: .github/copilot-instructions.md -->
<!-- version: 2.4.0 -->
<!-- guid: 4d5e6f7a-8b9c-0d1e-2f3a-4b5c6d7e8f9a -->
<!-- last-edited: 2026-06-13 -->

# apt-cacher-go — Additional Context

Org-wide coding standards (file headers, language rules, commit format) are at
**https://github.com/falkcorp/.github** and apply automatically to this repo.

For full project context: **CLAUDE.md** at the repo root.

## Project overview

Golang rewrite of apt-cacher-ng — a caching proxy for Debian/Ubuntu apt packages.

## Key directories

| Directory | Purpose |
|---|---|
| `cmd/` | Entry points: `serve` (proxy server), `admin`, `benchmark` |
| `internal/` | Core internals: cache, config, keymanager, mapper, metrics, parser, queue, security, server, storage |
| `pkg/` | (currently empty / shared utilities) |
| `integration/` | Integration tests |
| `scripts/` | Build and utility scripts |

## Critical constraints

- This is a **caching proxy** — correctness of HTTP cache semantics is critical
- All git operations must use conventional commit format: `type(scope): description`
- File headers are mandatory on every file created or modified
