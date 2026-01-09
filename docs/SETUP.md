# Setup Guide

## Quick Install (Recommended)

In Claude Code:

```
/plugin marketplace add Dammyjay93/claudepm
/plugin install claudepm
/claudepm:setup
```

Restart Claude Code after installing.

---

## Post-Setup Configuration

After running `/claudepm:setup`, add this to your `~/.claude/CLAUDE.md`:

```markdown
# Memory Protocol (ClaudePM)

Persistent memory across sessions. Multi-session safe.

## Workspace

@~/Vault/_manifest.md

## Session Start

1. Read manifest above
2. Check `Last Touched` for project hint
3. Prompt: "Resume {project}? (y / switch / list)"
4. Load project's `_index.md` for epic/task state

## Commands

- `/claudepm` — Smart dispatcher
- `/claudepm plan` — Create project from conversation
- `/claudepm start` — Mark task in-progress
- `/claudepm done` — Mark task complete
- `/claudepm save` — Save session
- `/claudepm switch` — Change project
```

The `@~/Vault/_manifest.md` line imports your workspace manifest automatically on every session.

---

## Verify Installation

Start a new Claude Code session and run:

```
/claudepm:status
```

You should see:

```
CLAUDEPM

No active project.

Projects: None yet
Sessions: None yet

Use /claudepm:plan to create a project from conversation.
```

---

## Vault Structure

After setup, your vault looks like:

```
~/Vault/
├── _manifest.md           # Project registry
├── .schemas/              # File templates
├── Projects/              # Your projects
└── Sessions/              # Session logs
```

---

## Troubleshooting

### Command not found

1. Check plugin is installed: `/plugin list`
2. Restart Claude Code to pick up new commands

### Manifest not loading

1. Check file exists: `ls ~/Vault/_manifest.md`
2. Check CLAUDE.md has the import: `@~/Vault/_manifest.md`

### Context not resuming

1. Check CLAUDE.md includes the session start instructions
2. Verify manifest has `Last Touched` set to your project

---

## Updating

```
/plugin marketplace update claudepm-marketplace
```

Restart Claude Code after updating.
