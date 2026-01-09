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
  <a href="#comparison">Comparison</a> •
  <a href="#documentation">Documentation</a>
</p>

<p align="center">
  ClaudePM turns your conversations into structured projects by automatically generating PRDs, epics, and tasks from what you discuss. It tracks your progress and captures decisions as you work, making them available to future sessions. This enables Claude to maintain continuity of your project state — knowing your current task, past decisions, and what's next — even after sessions end.
</p>

---

## Quick Start

```
/plugin marketplace add Dammyjay93/claudepm
/plugin install claudepm
/claudepm:setup
```

Restart Claude Code. Your project context will load automatically in future sessions.

---

## Key Features

- **Automatic Project Generation** — Discuss what you want to build, run `/claudepm:plan`, and ClaudePM generates a PRD with organized epics and tasks from your conversation
- **Session State Persistence** — Claude automatically loads your project context when you start a new session, including current task and recent decisions
- **Progress Tracking** — Mark tasks complete with `/claudepm:done`, track completion across epics, and always know what's next
- **Decision Capture** — Technical choices and constraints are stored in structured files (`rules.md`, `_index.md`) and loaded with your project
- **Multi-Project Support** — Maintain multiple projects simultaneously, each with its own state, and switch between them with `/claudepm:switch`
- **Session History** — Every session is logged with summaries, decisions made, and tasks completed for future reference
- **Local & Portable** — All data lives in `~/Vault/` as plain markdown files. No API keys, no external services, works offline

---

## How It Works

**Workflow:**

1. **Plan** — Discuss your project with Claude, then run `/claudepm:plan` to generate structure
2. **Work** — Start tasks with `/claudepm:start`, Claude loads relevant context automatically
3. **Track** — Mark tasks complete with `/claudepm:done`, progress updates across files
4. **Save** — Run `/claudepm:save` to log what happened before ending your session
5. **Resume** — Next session, Claude loads your project state and picks up where you left off

**Architecture:**

```
~/Vault/
├── _manifest.md              # Project registry + last-touched state
├── Projects/
│   └── my-app/
│       ├── _index.md         # Current epic, task, key decisions
│       ├── PRD.md            # Generated requirements
│       ├── rules.md          # Captured constraints
│       └── Epics/
│           └── 01-foundation.md  # Tasks + approach notes
└── Sessions/
    └── 2026-01-08.md         # Session log
```

**Components:**

1. **Manifest Registry** — `_manifest.md` tracks all projects and hints at which was last touched
2. **Project Index** — Each project's `_index.md` holds current state, active stances, and key decisions
3. **Epic Files** — Tasks organized by epic with status tracking and approach notes
4. **Session Logs** — Daily files capturing what happened for audit and context
5. **Smart Dispatcher** — `/claudepm` reads context and determines what action you need

---

## Commands

| Command | Description |
|---------|-------------|
| `/claudepm` | Smart dispatcher — reads context and suggests appropriate action |
| `/claudepm:setup` | Initialize vault structure at `~/Vault/` |
| `/claudepm:plan` | Generate PRD, epics, and tasks from current conversation |
| `/claudepm:start` | Begin working on next task, loads relevant context |
| `/claudepm:done` | Mark current task complete, updates progress, suggests next |
| `/claudepm:save` | Write session notes with summary and decisions |
| `/claudepm:status` | Display current project, epic, task, and blockers |
| `/claudepm:switch` | Change to a different project |

---

## Comparison

| | ClaudePM | Linear/Notion MCP |
|-|----------|-------------------|
| **Purpose** | Project state tracking for Claude Code | Integration with external tools |
| **Setup** | No API keys required | API keys required |
| **Task Creation** | Generated from conversation | Created manually in external tool |
| **Progress Tracking** | Built-in epics and task completion | Via external tool |
| **Decision Capture** | Structured in rules.md and _index.md | Varies by tool |
| **Storage** | Local markdown in ~/Vault/ | External service |
| **Offline Support** | Yes | No |

**ClaudePM** — Lightweight project continuity built for Claude Code. Generates structure from conversations, tracks progress across sessions, no external dependencies.

**Linear/Notion MCP** — Integration layer for existing project management tools. Use if you already manage projects in Linear or Notion and want Claude to read/write to them.

---

## Documentation

- **[Commands Reference](docs/COMMANDS.md)** — Detailed command documentation and usage examples
- **[Setup Guide](docs/SETUP.md)** — Installation, configuration, and troubleshooting
- **[Future: Obsidian](docs/FUTURE.md)** — Planned visual integration with Obsidian
- **[Changelog](CHANGELOG.md)** — Version history and release notes
- **[Contributing](CONTRIBUTING.md)** — Development setup and contribution guidelines

---

## Updating

```
/plugin marketplace update claudepm-marketplace
```

Restart Claude Code after updating to apply changes.

---

## License

This project is licensed under the **MIT License**.

See the [LICENSE](LICENSE) file for details.
