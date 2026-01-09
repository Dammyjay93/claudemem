---
description: Create a project from the current conversation - generates PRD, epics, and tasks
allowed-tools: Read, Write, Bash, Glob
argument-hint: [project-name]
---

# ClaudeMem Plan

Create a structured project from the conversation.

**Multi-session safe**: Creates new project files. Other sessions are unaffected.

## Steps

1. **Analyze Conversation**
   - Identify the product/feature being discussed
   - Extract requirements, decisions, and scope
   - Determine technical approach

2. **Generate Project ID**
   - Use argument if provided: `$ARGUMENTS`
   - Otherwise derive from project name (kebab-case)
   - Verify no duplicate exists in `~/Vault/Projects/`

3. **Detect Repository Location**
   - Check if current working directory contains `.git` → use cwd as repository
   - If no git repo detected, ask user: "Where is the code for this project? (path or 'none')"
   - If user says 'none' or project has no code yet → omit repository field
   - **NEVER guess paths like `/work/{id}`** — always detect or ask

4. **Create Project Structure**

```bash
mkdir -p ~/Vault/Projects/{id}/Epics
```

5. **Create Files**

### _index.md
```yaml
---
type: project
id: {id}
name: {Name}
status: active
priority: P1
created: {today}
brief: {1-2 sentence summary}
repository: {path}  # ONLY include if detected from cwd or provided by user
stack: [{technologies}]
---

# {Project Name}

## Overview
{Brief description}

## Current State
- **Active Epic**: {first epic or "None"}
- **Active Task**: {first task or "None"}
- **Blockers**: None

## Active Stances

| Domain | Stance | Source |
|--------|--------|--------|
| {domain} | {current stance} | rules.md §{section} |

## Key Decisions

| Decision | Rationale | Revisit if |
|----------|-----------|------------|
| {decision} | {why} | {conditions for reconsideration} |

## Epics
{List of epics with progress counts}

## Quick Links
- [PRD](./PRD.md)
- [Rules](./rules.md)
```

### PRD.md
```yaml
---
type: prd
project: {id}
version: 1
created: {today}
---

# {Project Name}

## Problem
{What problem does this solve}

## Solution
{High-level solution}

## Requirements
{Extracted from conversation}

## Non-Goals
{What we're explicitly not doing}

## Technical Approach
{Stack, architecture decisions}
```

### rules.md
```yaml
---
type: rules
project: {id}
updated: {today}
---

# Rules

Enforced constraints. Update in place, never append.

## Product
- {product constraint}

## UI
- {ui pattern/rule}

## Engineering
- {engineering standard}
```

### Epics
Create epic files based on logical groupings:
- `01-{name}.md` - Foundation/setup
- `02-{name}.md` - Core functionality
- etc.

Each epic contains:
- Description
- Approach section (epic-scoped decisions)
- Tasks as checkboxes
- Acceptance criteria

```yaml
---
type: epic
id: {id}
project: {project-id}
status: pending
priority: {P0/P1/P2}
created: {today}
---

# {Epic Name}

## Description
{What this epic accomplishes}

## Approach (this epic)
- {Epic-scoped decision or approach}

## Tasks
- [ ] {Task} #pending #{priority}

## Acceptance Criteria
- [ ] {Criterion}
```

6. **Update Manifest**
   - Add project to Projects table
   - Set `Last Touched` → new project
   - Update timestamp

7. **Announce Result**

```
PROJECT CREATED: {Name}

{Brief}

Epics:
1. {Epic 1} ({n} tasks)
2. {Epic 2} ({n} tasks)
...

Total: {n} epics, {m} tasks

Ready to start? First task: {first task}
```

## What Gets Created/Updated

| File | Action |
|------|--------|
| `Projects/{id}/_index.md` | Created with Active Stances, Key Decisions |
| `Projects/{id}/PRD.md` | Created |
| `Projects/{id}/rules.md` | Created with Product/UI/Engineering sections |
| `Projects/{id}/Epics/*.md` | Created with Approach sections |
| `_manifest.md` | Add to Projects table, set Last Touched |

## Rules

- Extract from conversation, don't invent
- Be specific in task descriptions
- Include acceptance criteria for epics
- Set realistic priorities (not everything is P0)
- If unclear, ask before creating
- Populate rules.md with any constraints identified
- Key Decisions should have revisit triggers

## Argument

$ARGUMENTS
