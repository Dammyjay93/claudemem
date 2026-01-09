# Manifest Schema

## File Location
`_manifest.md` (root of Vault)

## Purpose
Central registry for projects. Does NOT track active session state — that lives in each project's `_index.md`. Session history lives in `Sessions/` folder.

## Required Frontmatter

```yaml
---
type: manifest
version: 3
updated: string  # ISO timestamp
---
```

## Required Sections

```markdown
# Workspace

## Last Touched
project: {project-id}   # Advisory hint only, may be stale

## Projects
| id | name | status | priority | last_active | path |
|----|------|--------|----------|-------------|------|

## Blockers
| id | description | blocking | created | resolved |
|----|-------------|----------|---------|----------|

## Quick Stats
- Total projects: {n}
- Active projects: {n}
```

## Rules

1. **No active session state** — Don't store epic/task here. That's per-project.
2. **Last Touched is advisory** — It's a convenience hint for session start, not authoritative.
3. **Update Last Touched only on**:
   - Session start (when project is chosen)
   - Explicit `/claudemem switch`
4. **Update last_active** — When saving a session, update the project's `last_active` date.
5. **Session history** — Lives in `Sessions/` folder, not in manifest. No duplication.

## Multi-Session Behavior

Multiple Claude sessions can run simultaneously on different projects without conflict because:
- Each project's `_index.md` owns its active epic/task state
- Sessions only write to their own project file during work
- Manifest is only touched on explicit actions, not continuous updates
