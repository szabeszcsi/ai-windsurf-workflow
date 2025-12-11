---
name: plan-task
description: Plan implementation and create task file. Reads architecture & summaries, creates phased task file for multi-session work.
auto_execution_mode: 0
---

# Plan Task

Create an implementation plan before coding. Uses existing documentation to plan efficiently.

**Use when:**
- New feature implementation
- Changes touching multiple modules
- Architectural changes
- Unfamiliar with codebase area

**Skip when:**
- Single-file bug fix
- Trivial changes
- Already have clear plan

---

## Step 1: Understand the Request

Clarify what needs to be built:

| Question | Answer |
|----------|--------|
| What is the feature/change? | {description} |
| Why is it needed? | {business reason} |
| What's the scope? | {files/modules affected} |

---

## Step 2: Load Architecture

Read project structure:

```
1. SOLUTION_ARCHITECTURE.md    → Overall structure
2. PROJECT_STATUS.md           → Current state (if exists)
```

**If `SOLUTION_ARCHITECTURE.md` doesn't exist:**
→ Run `/generate-architecture` first

---

## Step 3: Load Tech Summaries

Check `docs/tech-summaries/` for relevant modules:

```bash
ls docs/tech-summaries/
```

### If summaries exist:

Read summaries for affected modules:
```
docs/tech-summaries/{layer}/_index.md    → Layer overview
docs/tech-summaries/{layer}/{module}.md  → Module details
```

**Benefits:** ~2KB per module vs ~50KB full source

### If summaries don't exist:

```
⚠️ No tech summaries found for: {modules}

Options:
[1] Generate summaries first (/generate-tech-summary)
[2] Proceed without (will read full source)
[3] Create minimal summary during planning

Recommended: Option 1 for complex modules, Option 2 for simple ones
```

---

## Step 4: Validate Summaries (Staleness Check)

For each summary loaded, quick validation:

```
Checking summary freshness...

For {module}:
- Summary date: {date from file}
- Key exports listed: {count}
- Quick source check: {matches/mismatch}
```

**If mismatch detected:**
```
⚠️ STALE SUMMARY: {module}

Summary shows: {what summary says}
Source shows: {what code actually has}

Options:
[1] Regenerate summary now (/generate-tech-summary)
[2] Note discrepancy and continue
[3] Abort planning until fixed

Recommended: Option 1 if significant, Option 2 if minor
```

---

## Step 5: Identify Dependencies

Based on summaries and architecture:

| This Change | Affects | Because |
|-------------|---------|---------|
| {component} | {other component} | {uses/imports} |
| {component} | {tests} | {needs test updates} |

---

## Step 6: Create Implementation Plan

```markdown
## Implementation Plan: {Feature Name}

**Scope:** {brief description}
**Estimated effort:** {hours/phases}

### Files to Create
| File | Purpose | ~Lines |
|------|---------|--------|
| `{path}` | {purpose} | {estimate} |

### Files to Modify
| File | Changes | Risk |
|------|---------|------|
| `{path}` | {what changes} | {low/med/high} |

### Implementation Order
1. {First step} - {why first}
2. {Second step} - {depends on 1}
3. {Third step} - {depends on 2}

### Testing Strategy
- Unit tests: {what to test}
- Integration: {if needed}

### Risks & Considerations
- {Risk 1}
- {Risk 2}
```

---

## Step 7: Create Task File

For multi-phase work, create the task file:

**File:** `docs/tasks/{feature}_tasks.md`

**Template:** `.ai/templates/TASK_FILE_TEMPLATE.md`

### Task File Structure

```markdown
# Task: {Feature Name}

**Developer:** {Name}
**Branch:** `feature/{feature-name}`
**Status:** 📋 Ready

---

## Overview

{2-3 sentence description}

---

## 🔒 Task Constants Tracking

| Item | Value | Established | Status |
|------|-------|-------------|--------|
| *Add as phases progress* | | | |

---

## Phases

### Phase 1: {Name}
**Goal:** {Specific, measurable goal}

**Create:**
| File | Purpose |
|------|---------|
| `{path}` | {purpose} |

**Success Criteria:**
- [ ] {criterion}
- [ ] Tests passing

---

### Phase 2: {Name}
...

---

## Success Criteria (Overall)

**Must Have:**
- {core requirement}

**Should Have:**
- {enhanced feature}
```

### After Creating Task File

1. Update `dev_context.md`:
   ```markdown
   ## 🎯 Primary Task
   **{Feature}** - Phase 1 📋
   - Task file: `docs/tasks/{feature}_tasks.md`
   ```

2. Create Phase 1 handoff if starting immediately:
   `docs/tasks/{feature}_phase1_handoff.md`

---

## Step 8: Confirm Plan

```
📋 TASK PLANNED

Feature: {name}
Phases: {count}
Estimated effort: {time}

Files to create:
- docs/tasks/{feature}_tasks.md
- docs/tasks/{feature}_phase1_handoff.md (if starting now)

Tech summaries: {loaded/missing/stale}

Ready to proceed?
[C] Create task file and start Phase 1
[T] Create task file only (start later)
[R] Revise plan
[A] Abort
```

---

## Output

When task file is created:

```
✅ TASK FILE CREATED

Task: docs/tasks/{feature}_tasks.md
Phases: {N} planned
Branch: feature/{feature-name}

{If starting now:}
Handoff: docs/tasks/{feature}_phase1_handoff.md
Updated: dev_context.md

Ready to implement Phase 1!

{If deferred:}
To start later, run /start-session and select this task.
```

---

## Quick Reference

| Input | Source |
|-------|--------|
| Project structure | `SOLUTION_ARCHITECTURE.md` |
| Module APIs | `docs/tech-summaries/{layer}/{module}.md` |
| Current state | `PROJECT_STATUS.md`, dev context (see `.windsurf/team.md`) |

| Output | Location |
|--------|----------|
| Task file | `docs/tasks/{feature}_tasks.md` |
| Phase handoff | `docs/tasks/{feature}_phase{N}_handoff.md` |
| Context update | `dev_context.md` |