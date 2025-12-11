# Update Context Workflow

Save progress mid-session without completing a phase.

---

## When to Use

- Made progress but phase not done
- Session ending (time, context running high)
- Want a checkpoint before risky change
- Switching to different task temporarily

**Don't use when:** Phase is complete → use `/phase-complete` instead

---

## Step 1: Identify Work Type

```
📝 SAVING PROGRESS

What type of work?
[P] Primary phase task
[L] Lingering task (bug/ad-hoc)
[N] New issue discovered
```

---

## Step 2: Gather Summary

Ask yourself / user:
- What was accomplished?
- What's the current status? (% complete, blocked, etc.)
- What's the immediate next step?

---

## Step 3: Check for New Task Constants

**Did we create anything that future sessions must NOT break?**

Examples:
- Test script with specific setup
- Constructor/method signature that must stay stable
- Config structure key
- Fixture file

If yes → Add to Task Constants section in dev_context.md

---

## Step 4: Update dev_context.md

### For PRIMARY task:
```markdown
## 🎯 Primary Task
**{Task Name}** - Phase {N} 🚧
- ✅ {completed item}
- 🚧 {in progress item}
- [ ] {remaining item}
**Status:** {X}% complete
**Next:** {immediate next step}
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

## Step 5: Create Session Doc (if significant work)

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

## Current Status
{Complete / In Progress / Blocked}

## Next Steps
- [ ] {next item}
```

---

## Step 6: Check File Size

| dev_context.md Size | Action |
|---------------------|--------|
| < 1.5 KB | ✅ OK |
| 1.5-2 KB | ⚠️ Consider archiving old sessions |
| > 2 KB | 🚨 Archive NOW before continuing |

**Archive process:**
1. Move old session summaries to `docs/archive/`
2. Keep only recent (last 3) completions
3. Keep current task and lingering items

---

## Step 7: Confirm Save

```
✅ CONTEXT SAVED

Updated:
- dev_context.md
- docs/working/{session_doc}.md (if created)

Work type: {Primary/Lingering/New}
Status: {status}
File size: {X} KB

Next session prompt:
---
I'm {name}. Continue {task description}.
Read dev_context.md for current state.
Branch: {branch}
Last: {what we just did}
Next: {immediate next step}
---
```

---

## Lingering Task Management

### Priority Levels
- 🔴 **Critical** - Blocking work, fix immediately
- 🟡 **High** - Should fix soon
- 🟢 **Medium** - Fix when convenient
- ⚪ **Low** - Backlog

### When to Promote to Task File
If lingering item:
- Takes >2 sessions to fix
- Requires >200 lines of new code
- Affects multiple components
- Needs formal testing

→ Create task file using `.ai/templates/TASK_FILE_TEMPLATE.md`

### Cleanup
When lingering task DONE:
- Move from Lingering to Recent Completions
- Archive/delete session doc
