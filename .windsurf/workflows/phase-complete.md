# Phase Complete Workflow

Protocol for completing a phase before committing.

---

## 🚨 HARD STOP

```
🚨 STOP - PHASE COMPLETE - DO NOT COMMIT YET
```

---

## Pre-Check

Before proceeding, verify:

1. **Context check** - Ask user for `/context` result
2. **Tests passing** - All tests must pass
3. **Correct branch** - Verify with `git branch --show-current`
4. **Direct memory** - Am I working from actual session memory? (If checkpoint-only → STOP)

---

## Required Steps (All Must Complete)

| # | Action | Output |
|---|--------|--------|
| 1 | Gather info | Component, phase #, developer, description |
| 2 | Run tests | `pytest` or equivalent → must pass |
| 3 | Verify branch | `git branch --show-current` |
| 4 | Create completion doc | `docs/tasks/{component}_phase{N}_complete.md` |
| 5 | Create handoff doc | `docs/tasks/{component}_phase{N+1}_handoff.md` |
| 6 | Update dev_context.md | Current state, Task Constants |
| 7 | Archive old handoff | Move to `docs/tasks/completed/` |
| 8 | Git commit & push | Only after steps 4-7 |
| 9 | Provide new session prompt | Ready-to-paste for next chat |

---

## Step 4: Completion Doc Template

**File:** `docs/tasks/{component}_phase{N}_complete.md`

```markdown
# {Component} Phase {N} Complete

**Date:** {date}
**Developer:** {name}
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

---

## Step 5: Handoff Doc

**File:** `docs/tasks/{component}_phase{N+1}_handoff.md`

Use template: `.ai/templates/HANDOFF_TEMPLATE.md`

**Must include:**
- Current status (what's done)
- Phase N+1 goals
- Components to create (with file paths)
- Implementation steps
- Success criteria
- **Task Constants** - copy from dev_context.md!

---

## Step 6: Update dev_context.md

```markdown
## ✅ Recent Completions (Last 3)
1. ✅ **Phase {N} - {Name}** ({date})
   - {Component1} ({X} lines, {Y} tests)

## 🎯 Primary Task
**{Task Name}** - Phase {N+1} 🔜
See: docs/tasks/{component}_phase{N+1}_handoff.md

## 🌿 Branch
`{branch}` - pushed
```

**Task Constants handling:**
- Non-final phase: Keep constants, copy to handoff
- Final phase: Archive to completion doc, remove from dev_context.md

---

## Final Phase Special Handling

**If this is the LAST phase of a task:**

1. **No handoff doc needed** (no next phase)
2. **Archive Task Constants** to completion doc:
   ```markdown
   ## 🔒 Task Constants (Archived)
   These were the key invariants for this task:
   {copy from dev_context.md}
   ```
3. **Remove 🔒 section** from dev_context.md
4. **Context file should shrink** back to normal size

---

## Checklist (All Must Be ✅)

- [ ] Context health checked
- [ ] Tests passing
- [ ] Completion doc created
- [ ] Handoff doc created (unless final phase)
- [ ] dev_context.md updated
- [ ] Task Constants preserved (or archived if final)
- [ ] Old handoff archived
- [ ] Git committed and pushed
- [ ] New session prompt provided

---

## Final Output

```
🎉 Phase {N} Complete!

✅ Created: docs/tasks/{component}_phase{N}_complete.md
✅ Created: docs/tasks/{component}_phase{N+1}_handoff.md
✅ Updated: dev_context.md
✅ Committed and pushed to {branch}

⚠️ START PHASE {N+1} IN A NEW CHAT

New session prompt:
---
I'm {name}. Continue {Task} Phase {N+1}.
Read dev_context.md and docs/tasks/{component}_phase{N+1}_handoff.md
Branch: {branch}
---
```
