---
description: Save session notes and update manifest
allowed-tools: Read, Write, Edit, Bash
---

# ClaudePM Save

## CRITICAL: Exhaustive Saves Are Mandatory

Every `/claudepm:save` MUST update ALL of the following files. No shortcuts. No partial saves.

**Multi-session safe**: Updates your project's files. Other sessions' states are unaffected.

## Required Files Checklist

Before announcing save completion, verify EVERY item:

- [ ] `~/Vault/_manifest.md` - Active context, last_active date, Recent Sessions table
- [ ] `~/Vault/Projects/{id}/_index.md` - Current State, Key Decisions, updated timestamp
- [ ] `~/Vault/Projects/{id}/Epics/{active}.md` - Task checkboxes, status, approach
- [ ] `~/Vault/Projects/{id}/rules.md` - If new constraints established
- [ ] `~/Vault/Sessions/{YYYY-MM-DD}-{project}.md` - Detailed session notes

## Steps

### 1. Gather Session Data

Read ALL of these files first:
- `~/Vault/_manifest.md` - Current active context
- `~/Vault/Projects/{id}/_index.md` - Project state
- `~/Vault/Projects/{id}/rules.md` - Current constraints
- `~/Vault/Projects/{id}/Epics/{active}.md` - Active epic tasks

Then review conversation for:
- What was built/changed/explored
- Decisions made (and their type - see Decision Routing)
- Tasks completed
- Files created or modified
- What's next

### 2. Update Project Index

**File**: `~/Vault/Projects/{id}/_index.md`

Required updates:
- `updated:` frontmatter date → today's date
- **Current State** section:
  - Last Session → brief description with date
  - Blockers → any new blockers
  - Next → what should happen next
  - Pending Work → if multiple tracks exist
- **Key Decisions** table → add if major decision made (keep curated to ~10)
- **Active Stances** table → update if stance changed
- **Epic progress** → update task counts if applicable

### 3. Update Epic File

**File**: `~/Vault/Projects/{id}/Epics/{active}.md`

Required updates:
- Check off completed tasks with `[x]`
- Update task statuses (`#done`, `#in-progress`)
- Check off completed acceptance criteria
- Update **Approach** section with epic-scoped decisions
- Update epic `status:` frontmatter if changed (planned → in-progress → done)

### 4. Update Rules (If Needed)

**File**: `~/Vault/Projects/{id}/rules.md`

Only update if:
- A new enforced constraint was established
- An existing rule changed

Rules are update-in-place, NEVER append-only.

### 5. Create Session File

**File**: `~/Vault/Sessions/{YYYY-MM-DD}-{project}.md`

Session files must be DETAILED, not summaries. Include:

```yaml
---
type: session
date: {YYYY-MM-DD}
project: {project id}
subproject: {if applicable, e.g., "mobile", "admin"}
---

# Session: {Project Name} - {Brief Topic}

## Summary
{2-3 sentence overview of what happened this session}

## Context
{Why this work was started, what triggered it}

## Exploration/Work Done
{Detailed description of what was explored, built, or changed}
{Include specific findings, numbers, file paths}

## Decisions
- **{Topic}**: {Decision and rationale}
- **{Topic}**: {Decision and rationale}

## Status
- [x] {Completed item}
- [x] {Completed item}
- [ ] {Pending item}

## Key Files
- `{path}` - {purpose}
- `{path}` - {purpose}

## Next Steps
1. {First priority with specific action}
2. {Second priority}
3. {Third priority}
```

### 6. Update Manifest

**File**: `~/Vault/_manifest.md`

Required updates:
- `## Active Context` → set to current project/epic/task
- Projects table → update `last_active` date for this project
- Recent Sessions table → add new row at TOP with today's summary

### 7. Announce (Exhaustive Format)

```
SESSION SAVED (EXHAUSTIVE)

Project: {name} ({subproject if applicable})
Session: {brief topic}

Files Updated:
  ~/Vault/_manifest.md
    - {specific change}
    - {specific change}

  ~/Vault/Projects/{id}/_index.md
    - {specific change}
    - {specific change}

  ~/Vault/Projects/{id}/Epics/{epic}.md
    - {specific change} (or "No changes - work not in this epic")

  ~/Vault/Sessions/{date}-{project}.md (created)
    - {key sections included}

Rules: {Updated | No changes}

Next: {first next step}
```

## Decision Routing

| Decision type | Where it goes | Growth pattern |
|---------------|---------------|----------------|
| Enforced constraint | `rules.md` | Update in place |
| Major product decision | `_index.md` Key Decisions | Curated (max ~10) |
| Current stance | `_index.md` Active Stances | Update in place |
| Epic-specific approach | Epic file Approach section | Lives with epic |
| Context/rationale | Session notes | Accumulates naturally |

## Auto-Save Triggers

Save when:
- User says "done for today" / "stopping" / "save"
- Switching to a different project
- Before `/claudepm switch`
- Significant milestone reached
- User explicitly requests save

## Common Mistakes to Avoid

1. **Skipping manifest updates** - Always update Active Context and Recent Sessions
2. **Minimal session files** - Session files are historical record, be detailed
3. **Forgetting frontmatter dates** - Update `updated:` in _index.md
4. **Not updating last_active** - Projects table needs today's date
5. **Announcing before completing** - Verify ALL files updated before announcing
