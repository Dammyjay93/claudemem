# Changelog

All notable changes to ClaudePM will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [3.0.0] - 2026-01-09

### Changed
- **BREAKING**: Renamed plugin from `claudemem` to `claudepm`
- All commands now use `/claudepm:*` prefix instead of `/claudemem:*`
- Repository renamed from `claudemem` to `claudepm`
- Updated description to emphasize project management focus

### Migration
Users need to reinstall with new name:
```
/plugin marketplace remove claudemem-marketplace
/plugin marketplace add Dammyjay93/claudepm
/plugin install claudepm
```

## [2.0.0] - 2026-01-09

### Added
- **Bounded decision system**: Decisions now route to specific locations
  - `rules.md` for enforced constraints (update in place)
  - `Active Stances` table in `_index.md` (pointers to rules)
  - `Key Decisions` table in `_index.md` (curated max ~10)
  - `Approach` section in epic files (epic-scoped)
  - Session notes for full context history
- Explicit file structure documentation in all commands
- Full paths for epic files: `~/Vault/Projects/{project}/Epics/{epic}.md`

### Changed
- Replaced `Decisions.md` (unbounded append-only) with bounded system
- Exhaustive save protocol now updates all relevant files
- Commands now specify exact file paths to prevent path guessing errors

### Fixed
- Repository path detection in `/claudepm:plan` - now detects from cwd or asks user
- `${CLAUDE_PLUGIN_ROOT}` not expanding in markdown commands - use full marketplace path

## [1.0.0] - 2026-01-08

### Added
- Initial release
- Multi-session support (B-lite architecture)
- Project, epic, and task management
- Session continuity across Claude Code sessions
- Commands: plan, start, done, save, status, switch
- Vault storage structure at `~/Vault/`
- Manifest-based project registry
