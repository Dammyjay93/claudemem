<h1 align="center">ClaudePM</h1>

<h4 align="center">Project state management for <a href="https://docs.anthropic.com/en/docs/claude-code" target="_blank">Claude Code</a>.</h4>

<p align="center">
  <a href="https://github.com/Dammyjay93/claudepm/actions/workflows/validate.yml">
    <img src="https://github.com/Dammyjay93/claudepm/actions/workflows/validate.yml/badge.svg" alt="Validate">
  </a>
  <a href="https://github.com/Dammyjay93/claudepm/releases">
    <img src="https://img.shields.io/github/v/release/Dammyjay93/claudepm" alt="Release">
  </a>
  <a href="LICENSE">
    <img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="License">
  </a>
  <a href="https://github.com/sponsors/Dammyjay93">
    <img src="https://img.shields.io/github/sponsors/Dammyjay93" alt="Sponsors">
  </a>
</p>

<p align="center">
  <a href="#quick-start">Quick Start</a> •
  <a href="#key-features">Key Features</a> •
  <a href="#how-it-works">How It Works</a> •
  <a href="#commands">Commands</a> •
  <a href="#documentation">Documentation</a>
</p>

<p align="center">
  ClaudePM organizes your conversations into structured projects with epics and tasks, then tracks your progress across sessions. When you start a new session, Claude loads your project context and knows exactly where you left off.
</p>

---

## Quick Start

```
/plugin marketplace add Dammyjay93/claudepm
/plugin install claudepm
/claudepm:setup
```

Restart Claude Code. Your project context will load automatically in future sessions.

**Key Features:**

- **Conversation to Structure** — Discuss what you want to build, run `/claudepm:plan`, get organized epics and tasks
- **Session Continuity** — Claude loads your project state automatically when you start a new session
- **Progress Tracking** — Mark tasks complete, see what's next, track where you are in each epic
- **Decision Capture** — Technical choices and constraints are stored and loaded with your project
- **Multi-Project Support** — Work on multiple projects, each maintains its own state
- **Session History** — Every session is logged with what happened and decisions made
- **Offline & Portable** — Everything is markdown files in `~/Vault/`. No API keys, no external services

---

## How It Works

**Core Components:**

1. **Vault Storage** — All project data lives in `~/Vault/` as plain markdown files
2. **Manifest Registry** — `_manifest.md` tracks your projects and last-touched state
3. **Project Index** — Each project's `_index.md` holds current epic, task, and key decisions
4. **Epic Files** — Tasks organized by epic with approach notes and completion status
5. **Session Logs** — Daily session files capture what happened for future reference
6. **Smart Dispatcher** — `/claudepm` command determines what action you need

**File Structure:**

```
~/Vault/
├── _manifest.md              # Project registry
├── Projects/
│   └── my-app/
│       ├── _index.md         # Active state + decisions
│       ├── PRD.md            # Requirements
│       ├── rules.md          # Constraints
│       └── Epics/
│           └── 01-foundation.md
└── Sessions/
    └── 2026-01-08.md         # Session history
```

---

## Commands

| Command | Description |
|---------|-------------|
| `/claudepm` | Smart dispatcher — determines what you need |
| `/claudepm:setup` | Initialize vault structure |
| `/claudepm:plan` | Convert conversation into PRD, epics, and tasks |
| `/claudepm:start` | Begin working on next task |
| `/claudepm:done` | Mark current task complete |
| `/claudepm:save` | Save session notes |
| `/claudepm:status` | View current project state |
| `/claudepm:switch` | Change active project |

---

## Documentation

- **[Changelog](CHANGELOG.md)** — Version history and updates
- **[Contributing](CONTRIBUTING.md)** — Development setup and guidelines

---

## Updating

```
/plugin marketplace update claudepm-marketplace
```

Restart Claude Code after updating.

---

## License

This project is licensed under the **MIT License**.

See the [LICENSE](LICENSE) file for details.
