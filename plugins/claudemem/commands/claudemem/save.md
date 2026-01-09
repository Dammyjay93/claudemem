---
description: Save session notes and update manifest
allowed-tools: Read, Write, Edit, Bash
---

# ClaudeMem Save

**EXHAUSTIVE SAVES REQUIRED** - Every save must touch ALL relevant files.

**Multi-session safe**: Updates your project's files. Other sessions' states are unaffected.

## Steps

1. **Gather Session Data**
   - Read `~/Vault/_manifest.md` for Last Touched project
   - Read project's `_index.md` for current state
   - Read project's `rules.md` for current constraints
   - Read active epic file for current tasks
   - Review conversation for:
     - What was built/changed
     - Decisions made (and what type)
     - Tasks completed
     - What's next

2. **Update Project Index** (`~/Vault/Projects/{id}/_index.md`)
   - Update **Current State** section (active epic/task, last completed)
   - Update **Epic progress counts** (e.g., "8/15 tasks")
   - Update **Active Stances** table if any stances changed
   - Update **Key Decisions** table if a major decision was made
     - Key Decisions are CURATED (max ~10), not appended
     - Remove outdated ones, add significant new ones

3. **Update Epic File** (`~/Vault/Projects/{id}/Epics/{active}.md`)
   - Check off ALL completed tasks with [x]
   - Update task statuses (#done, #in-progress)
   - Check off completed acceptance criteria
   - Update **Approach** section with epic-scoped decisions
   - Update epic status if changed (pending → in-progress → done)

4. **Update Rules if Needed** (`~/Vault/Projects/{id}/rules.md`)
   - If a new enforced constraint was established → add to appropriate section
   - If an existing rule changed → update in place
   - Rules are update-in-place, NEVER append-only
   - Sections: Product, UI, Engineering

5. **Create Session File** (`~/Vault/Sessions/{YYYY-MM-DD}-{project}.md`)

```yaml
---
type: session
date: {YYYY-MM-DD}
project: {project id}
---

# Session: {Project Name}

## Summary
{2-3 sentence summary}

## Completed
- {Task completed}
- {Another completed item}

## Decisions
- **{Topic}**: {Decision and brief rationale}

## Next Steps
- {First priority}
- {Second priority}
```

6. **Update Manifest** (`~/Vault/_manifest.md`)
   - Update project's `last_active` date in Projects table
   - Update `Last Touched` to current project

7. **Announce**

```
SESSION SAVED

Project: {name}
Completed: {n} tasks
Rules updated: {yes/no}
Next: {first next step}
```

## Decision Routing

When saving, route decisions to the right place:

| Decision type | Where it goes | Growth pattern |
|---------------|---------------|----------------|
| Enforced constraint | `rules.md` | Update in place |
| Major product decision | `_index.md` Key Decisions | Curated (max ~10) |
| Current stance | `_index.md` Active Stances | Update in place |
| Epic-specific approach | Epic file Approach section | Lives with epic |
| Context/rationale | Session notes | Accumulates naturally |

**Key principle**: Rules and stances are bounded. History lives in session files.

## Auto-Save Triggers

Consider saving when:
- User says "done for today" / "stopping" / "save"
- Switching to a different project
- Before `/claudemem switch`
- Significant milestone reached
