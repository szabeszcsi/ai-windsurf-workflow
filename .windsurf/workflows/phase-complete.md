---
name: phase-complete
description: Phase completion protocol. Run when all phase tasks and tests pass.
auto_execution_mode: 0
---

# Phase Complete

Run this workflow when a phase is done and all tests pass.

---

## Pre-Flight Check

Before proceeding, verify:

- [ ] All phase tasks completed
- [ ] All tests passing
- [ ] On correct feature branch
- [ ] No uncommitted experimental code

**If any unchecked:** Complete those first, then return.

---

## Step 1: Gather Info

Identify:

| Item | Value |
|------|-------|
| Component/Feature | {name} |
| Phase Number | {N} |
| Developer | {name} |
| Branch | {branch} |

---

## Step 2: Run Tests

```bash
pytest tests/unit/ -v
pytest tests/integration/ -v  # if applicable
```

**All tests must pass before continuing.**

---

## Step 3: Update Tech Summaries

Run `/generate-tech-summary` for each module created/modified this phase.

```
Layer: {layer}
Modules: {list modules from this phase}
```

**Why:** Fresh sessions load summaries (~2KB) instead of full source (~50KB).

See: `.windsurf/workflows/generate-tech-summary.md`

---

## Step 4: Create Documentation

### 4a. Completion Doc

Create `docs/tasks/{component}_phase{N}_complete.md`:

```markdown
# {Component} Phase {N} Complete

**Date:** {date}
**Developer:** {name}
**Branch:** `{branch}`

## Summary
{What was accomplished}

## Deliverables
| File | Lines | Purpose |
|------|-------|---------|
| `{path}` | {N} | {description} |

## Test Results
- {X} tests passing
- Coverage: {Y}%

## Key Decisions
- {Decision 1}
- {Decision 2}
```

### 4b. Next Phase Handoff (if not final phase)

Create `docs/tasks/{component}_phase{N+1}_handoff.md`

Use template: `.ai/templates/HANDOFF_TEMPLATE.md`

**Must include:**
- 🔒 Task Constants (copy from dev_context.md)
- Phase goals and deliverables
- Implementation steps

---

## Step 5: Update Context Files

### dev_context.md

```markdown
## ✅ Recent Completions
1. ✅ Phase {N} - {Name} ({date})

## 🎯 Primary Task
**{Task}** - Phase {N+1} 🚧
- Handoff: `docs/tasks/{component}_phase{N+1}_handoff.md`
```

### PROJECT_STATUS.md

Update Active Work and Recent Changes sections.

---

## Step 6: Archive Old Handoff

```bash
mv docs/tasks/{component}_phase{N}_handoff.md docs/tasks/completed/
```

---

## Step 7: Git Commit

```bash
git add .
git commit -m "feat({component}): Complete Phase {N} - {description}"
git push origin {branch}
```

---

## Step 8: Final Report

```
🎉 PHASE {N} COMPLETE

✅ Completion doc: docs/tasks/{component}_phase{N}_complete.md
✅ Tech summaries: Updated
✅ Handoff doc: docs/tasks/{component}_phase{N+1}_handoff.md
✅ Context files: Updated
✅ Git: Committed and pushed

⚠️ START PHASE {N+1} IN A NEW CHAT

Copy this to start:
---
Run /start-session
Task: {Component} Phase {N+1}
Branch: {branch}
---
```

---

## Final Phase Handling

If this is the **LAST phase** of a task:

1. **No handoff doc needed**
2. **Archive Task Constants** to completion doc:
   ```markdown
   ## 🔒 Task Constants (Archived)
   {copy from dev_context.md}
   ```
3. **Remove 🔒 section** from dev_context.md
4. **Update PRIMARY task** to next task or "None"

---

## Checklist

- [ ] Tests passing
- [ ] Tech summaries updated
- [ ] Completion doc created
- [ ] Handoff doc created (unless final)
- [ ] dev_context.md updated
- [ ] PROJECT_STATUS.md updated
- [ ] Old handoff archived
- [ ] Git committed and pushed
- [ ] New chat prompt provided