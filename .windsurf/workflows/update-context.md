---
name: update-context
description: Save progress mid-session. Use when you've made progress but phase isn't complete.
auto_execution_mode: 0
---

# Update Context

Save progress mid-session without completing a phase.

**Use when:** Made progress, session ending, want checkpoint, switching tasks  
**Don't use when:** Phase is complete → use `/phase-complete` instead

---

## Step 1: Identify Developer

**If `.windsurf/team.md` exists:** Confirm which developer's context to update.

| Developer | Context File |
|-----------|--------------|
| {Name 1} | dev1_context.md |
| {Name 2} | dev2_context.md |

**Single-developer:** Use `dev_context.md`

---

## Step 2: Classify Work Type

```
📝 SAVING PROGRESS

What type of work?
[P] Primary phase task
[L] Lingering task (bug/ad-hoc)
[N] New issue discovered
```

---

## Step 3: Gather Summary

For each work item:
- What was accomplished?
- What's the status? (% complete, blocked, etc.)
- What's the immediate next step?

---

## Step 4: Check for New Task Constants

**Did we create anything that future sessions must NOT break?**

Examples:
- Test script with specific setup
- Constructor/method signature that must stay stable
- Config structure key
- Fixture file

**If yes:** Add to `🔒 Task Constants` section in dev_context.

---

## Step 5: Update Context File

### For PRIMARY task:

```markdown
## 🎯 Primary Task
**{Task Name}** - Phase {N} 🚧
- ✅ {completed item}
- 🚧 {in progress item}
- [ ] {remaining item}

Status: {X}% complete
Next: {immediate next step}
Handoff: `docs/tasks/{component}_phase{N}_handoff.md`
```

### For LINGERING task:

```markdown
## 🔥 Lingering Tasks
1. **{Bug/Issue}** - {🔴/🟡/🟢} {✅/🚧}
   - {brief description}
   - Progress: {what was done}
   - Next: {what's next}
```

### For NEW discovered issue:

```markdown
## 🔥 Lingering Tasks
{N}. **{New Issue}** - 🆕 {priority}
   - Discovered: {date}
   - {brief description}
   - Recommend: {task file / immediate fix}
```

---

## Step 6: Create Session Doc (if significant work)

For non-trivial work, create: `docs/working/{task}_{date}.md`

```markdown
# {Task/Bug Name} Session

**Date:** {date}
**Developer:** {name}
**Type:** Bug Fix / Investigation / Feature

## What Was Done
- {item 1}
- {item 2}

## Files Modified
- `{path}` - {change}

## Status
{Complete / In Progress / Blocked}

## Next Steps
- [ ] {next item}
```

---

## Step 7: Check Context File Size

| Size | Action |
|------|--------|
| < 1.5 KB | ✅ OK |
| 1.5-2 KB | ⚠️ Archive old sessions soon |
| > 2 KB | 🚨 Archive NOW - move old completions to `docs/archive/` |

---

## Step 8: Confirm Save

```
✅ CONTEXT SAVED

Updated: {dev_context_file}
Work type: {Primary/Lingering/New}
Status: {status}
Size: {X} KB

Next session prompt:
---
Run /start-session
Continue: {task description}
Branch: {branch}
---
```

---

## Quick Reference

| Scenario | Update Section |
|----------|----------------|
| Phase progress | 🎯 Primary Task |
| Bug fix progress | 🔥 Lingering Tasks |
| New issue found | 🔥 Lingering Tasks (add new) |
| Task completed | Move to ✅ Recent Completions |
| New constant created | 🔒 Task Constants |