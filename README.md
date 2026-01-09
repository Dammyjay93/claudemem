# ClaudePM

[![Validate Plugin](https://github.com/Dammyjay93/claudepm/actions/workflows/validate.yml/badge.svg)](https://github.com/Dammyjay93/claudepm/actions/workflows/validate.yml)
[![GitHub release](https://img.shields.io/github/v/release/Dammyjay93/claudepm)](https://github.com/Dammyjay93/claudepm/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![GitHub Sponsors](https://img.shields.io/github/sponsors/Dammyjay93)](https://github.com/sponsors/Dammyjay93)

**Project management for Claude Code.** Track tasks, decisions, and session history across conversations.

```
[New session starts]

Claude: "Resuming your project. Currently on epic 2: 'Core Features'.
         Task: Set up database auth. Continue where you left off?"
```

---

## The Problem

Claude Code doesn't track project state between sessions. You can drop files for context, but:

- **What task am I on?** — No progress tracking
- **What did I decide yesterday?** — Decisions get lost in conversation history
- **What happened last session?** — No automatic session logging
- **Which project am I working on?** — Claude doesn't know which one is active

ClaudePM adds that layer. It auto-loads context, tracks tasks, and logs sessions.

---

## Quick Start

```
/plugin marketplace add Dammyjay93/claudepm
/plugin install claudepm
/claudepm:setup
```

---

## Commands

| Command | What It Does |
|---------|--------------|
| `/claudepm:setup` | Initialize vault structure |
| `/claudepm:plan` | Turn conversation into PRD, epics, and tasks |
| `/claudepm:start` | Start next task (or a specific one) |
| `/claudepm:done` | Mark task complete, get next suggestion |
| `/claudepm:save` | Write session notes before closing |
| `/claudepm:status` | Show active project and current task |
| `/claudepm:switch` | Change to a different project |

---

## Workflow

### Plan

Discuss what you want to build, then:

```
You: /claudepm:plan

Claude: Creates PRD, epics, tasks from conversation
        "Created 'my-project': 4 epics, 23 tasks. Ready to start?"
```

### Work

```
You: /claudepm:start

Claude: "Starting task: Set up database schema"
        [Loads context from PRD and previous decisions]

[Work on it]

You: /claudepm:done

Claude: "Marked complete. Next up: Implement user auth. Continue?"
```

### Resume

```
[Next day, open Claude Code]

Claude: "Resuming my-project. Current task: Implement user auth. Ready?"
```

---

## How It Works

Everything lives in `~/Vault/` as markdown files:

```
~/Vault/
├── _manifest.md                # Project registry
├── Projects/
│   └── my-project/
│       ├── _index.md           # Active state + decisions
│       ├── PRD.md              # Requirements
│       ├── rules.md            # Constraints
│       └── Epics/
│           ├── 01-foundation.md
│           └── 02-features.md
└── Sessions/
    └── 2026-01-08-project.md   # Session history
```

On session start, Claude reads `_manifest.md` for project context. Task state lives in each project's `_index.md`.

### Multi-Session Support

Multiple Claude sessions work on different projects simultaneously. Each writes to its own project file. No conflicts.

```
Terminal A (api-backend)        Terminal B (mobile-app)
         │                               │
         ▼                               ▼
 api-backend/_index.md          mobile-app/_index.md
```

---

## Comparison with Other Tools

| Feature | ClaudePM | Linear/Notion MCP | Manual PRD |
|---------|----------|-------------------|------------|
| Setup | No API keys | API keys required | None |
| Task generation | From conversation | Manual | Manual |
| Session memory | Automatic | External service | None |
| Offline | Yes | No | Yes |
| Multi-project | Yes | Depends | Manual |
| Decision tracking | Structured | Varies | None |

**Use ClaudePM if**: You want lightweight session memory without external dependencies.

**Use Linear/Notion MCP if**: You already use those tools and want Claude to interact with them.

---

## Updating

```
/plugin marketplace update claudepm-marketplace
```

Restart Claude Code after updating.

---

## Documentation

- [Commands Reference](docs/COMMANDS.md)
- [Setup Guide](docs/SETUP.md)
- [Changelog](CHANGELOG.md)

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## License

MIT
