---
name: phase-complete-templates
description: Templates for phase completion. Load only when executing /phase-complete
trigger: manual
---

# Phase Complete Templates

**Load this file when executing `/phase-complete` steps.**

---

## Step 2: Test Commands

```bash
pytest tests/unit/ -v
```

---

## Step 3: Branch Verification

```bash
git branch --show-current
git status --short
```

---

## Step 4: Completion Doc Template

**File:** `docs/tasks/{layer}_phase{N}_complete.md`

```markdown
# {Layer} Phase {N} Complete

**Date:** {Mon DD, YYYY}
**Developer:** {Name}
**Branch:** `{branch}`

## Summary
{Brief description of what was accomplished}

## Deliverables

| File | Lines | Description |
|------|-------|-------------|
| `{path}` | {N} | {description} |

## Test Results
- {X} tests passing
- Coverage: {Y}%

## Key Decisions
- {Decision 1}
- {Decision 2}
```

**If FINAL phase, add this section:**
```markdown
## 🔒 Task Constants (Archived)
These were the key invariants throughout this task:

| Item | Value | Established |
|------|-------|-------------|
| {item} | `{path/value}` | Phase {N} |

These can now be modified freely as the task is complete.
```

---

## Step 5: Handoff Doc

**File:** `docs/tasks/{layer}_phase{N+1}_handoff.md`

Use template: `docs/ai/TEMPLATES/HANDOFF_DOC_TEMPLATE.md`

**Must include:**
- Current status (what's done)
- Phase N+1 goals  
- Components to create (with file paths)
- Implementation steps with code examples
- Success criteria
- **🔒 Task Constants** - copy from dev context! Critical for continuity.

**Task Constants Section in Handoff:**
```markdown
## 🔒 Task Constants (DO NOT MODIFY)
These were established in earlier phases and MUST be preserved:

- **Test script:** `{path}` - DO NOT RECREATE
- **Constructor:** `{Class}({params})` - DO NOT CHANGE
- **Key decisions:** {list}
```

---

## Step 6: Dev Context Update

**File:** `dev{X}_context.md`

```markdown
## ✅ Recent Completions (Last 3)
1. ✅ **Phase {N} - {Name}** ({date})
   - {Component1} ({X} lines, {Y} tests)

## 🔧 Next
Phase {N+1} - {Name}
See: docs/tasks/{layer}_phase{N+1}_handoff.md

## 📍 Branch
`{branch}` - pushed
```

---

## Step 7: PROJECT_STATUS.md Updates

**Section 1 - Layer Status table:**
```markdown
| {Layer} | {new status} | {updated notes} |
```

**Section 2 - Active Work:**
```markdown
### {Name} (Developer {X}) - {Layer}
- **Branch:** `{branch}`
- **Status:** ✅ Phase {N} complete, ready for Phase {N+1}
- **Last:** Phase {N} - {description}
- **Next:** Phase {N+1} - {next phase name}
- **Context:** `dev{X}_context.md`
```

**Section 3 - Recent Changes (add to top):**
```markdown
- **{Mon DD}:** {Layer} Phase {N} complete - {brief description}
```

---

## Step 8: PROJECT_DETAILS.md Update

**Append to Change History:**
```markdown
**{Mon DD}:**
- {Layer} Phase {N} complete ({Developer})
- {Key deliverable 1}
- {Key deliverable 2}
- {X} tests, {Y} lines
```

---

## Step 9: Archive Command

```bash
mv docs/tasks/{layer}_phase{N}_handoff.md docs/tasks/completed/
```

---

## Step 10: Git Commands

```bash
git add .
git commit -m "feat({layer}): Complete Phase {N} - {description}"
git push origin {branch}
```

---

## Step 11: New Chat Prompt

Provide to user:
```
I'm {name}. Starting {Layer} Phase {N+1}.
Read dev{X}_context.md and docs/tasks/{layer}_phase{N+1}_handoff.md
```
