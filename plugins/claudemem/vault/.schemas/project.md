# Project Schema

## File Location
`Projects/{id}/_index.md`

## Required Frontmatter

```yaml
---
type: project
id: string           # kebab-case, unique (e.g., "recall", "townsquare")
name: string         # Human-readable name
status: string       # active | paused | completed | archived
priority: string     # P0 | P1 | P2
created: string      # ISO date (YYYY-MM-DD)
---
```

## Optional Frontmatter

```yaml
brief: string        # 1-3 sentence description
repository: string   # Path to code repository
stack: array         # Technologies used
target_date: string  # Target completion date
milestone: string    # Current milestone name
```

## Required Sections

```markdown
# {Project Name}

## Overview
{Brief description}

## Current State
- **Active Epic**: {epic name or "None"}
- **Active Task**: {task name or "None"}
- **Last Completed**: {last completed task}
- **Blockers**: {blocker list or "None"}

## Active Stances

| Domain | Stance | Source |
|--------|--------|--------|
| {domain} | {current stance} | rules.md §{section} |

## Key Decisions

| Decision | Rationale | Revisit if |
|----------|-----------|------------|
| {decision} | {why} | {conditions} |

## Epics
<!-- List of epics with progress counts -->

## Quick Links
- [PRD](./PRD.md)
- [Rules](./rules.md)
```

## Rules

1. One project = one folder in `Projects/`
2. Folder name must match `id` field
3. Never create duplicate project folders
4. `_index.md` is the entry point, always exists
5. **Current State is source of truth** — Active epic/task live here, not in manifest
6. **Active Stances** — Pointers to current rules, update in place
7. **Key Decisions** — Curated top ~10 decisions with revisit triggers, not append-only

## Related Files

| File | Purpose | Growth Pattern |
|------|---------|----------------|
| `rules.md` | Enforced constraints | Update in place |
| `PRD.md` | Product requirements | Update in place |
| `Epics/*.md` | Tasks and approach | Lives with epic |

## Multi-Session Note

The `Current State` section is where session state lives. When working on this project, update this file — not the manifest. This allows multiple Claude sessions to work on different projects simultaneously without conflict.

## Decision Routing

Decisions made during work should be routed:

| Decision type | Where it goes |
|---------------|---------------|
| Enforced constraint | `rules.md` |
| Major product decision | Key Decisions table (curated) |
| Current stance | Active Stances table |
| Epic-specific | Epic file Approach section |
| Full context | Session notes |
