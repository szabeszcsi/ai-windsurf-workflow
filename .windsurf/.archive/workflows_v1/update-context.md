---
description: Save progress mid-session. Usage: /update-context
auto_execution_mode: 1
---

# Update Context

**Use when:** Made progress but not done, session ending, want checkpoint  
**Don't use when:** Phase complete → use `/phase-complete`

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

Ask:
- What was accomplished?
- What's the status? (complete/in-progress/blocked)
- What's next?

---

## Step 3: Update Dev Context

### For PRIMARY task:
Update the `🎯 Active Task` section:
```markdown
## 🎯 Active Task
**{Task Name}** - Phase {N} 🚧
- ✅ {completed item}
- 🚧 {in progress}
- [ ] {remaining}
**Status:** {X}% complete
```

### Update 🔒 Task Constants (if new invariants created):
When you create something that MUST be preserved across phases:
```markdown
## 🔒 Task Constants (DO NOT MODIFY)
**Task:** {Task Name} (Phases 1-{N})

- **Test script:** `tests/integration/{test}.py` ← ADD NEW
- **Constructor:** `{Class}({params})` - DO NOT CHANGE ← ADD NEW
- **Key file:** `{path}` - created Phase {N} ← ADD NEW
```

**Ask yourself:** "Did I create anything this session that future phases must NOT break?"
- Test scripts with specific setup
- Constructor/method signatures
- Config structures
- Fixture files

### For LINGERING task:
Update/add to `🔥 Lingering` section:
```markdown
## 🔥 Lingering Tasks
1. **{Bug/Issue}** - {priority} {status}
   - {brief description}
   - See: `docs/working/{session_doc}.md`
2. **{Another issue}** - {priority}
```

### For NEW discovered issue:
Add to Lingering with flag:
```markdown
3. **{New Issue}** - 🆕 {priority}
   - Discovered: {date}
   - {brief description}
   - Recommend: {task file / immediate fix}
```

---

## Step 4: Create Session Doc (if significant work)

For non-trivial work, create: `docs/working/{task}_{YYYYMMDD}_{HHMM}.md`

```markdown
# {Task/Bug Name} Session
**Date:** {date time}
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

## Step 5: Update PROJECT_STATUS (Active Work only)

```markdown
### {Name} (Developer {X}) - {Layer}
- **Branch:** `{branch}`
- **Status:** {current status}
- **Last:** {what was just done}
- **Next:** {what's next}
- **Lingering:** {count} items
```

---

## Step 6: Check File Size

| Size | Action |
|------|--------|
| < 1.5 KB | ✅ OK |
| 1.5-2 KB | ⚠️ Archive old sessions |
| > 2 KB | 🚨 Archive NOW before continuing |

**Archive command:**
```bash
# Move old session content to archive
mv docs/archive/old_*.md docs/archive/
```

---

## Step 7: Confirm

```
✅ CONTEXT SAVED

Updated:
- dev{X}_context.md
- PROJECT_STATUS.md (Active Work)
- docs/working/{session_doc}.md (if created)

Work type: {Primary/Lingering/New}
Status: {status}
File size: {X} KB

Ready for next session! 🚀
```

---

## Lingering Task Management

### Priority Levels
- 🔴 **Critical** - Blocking work, fix immediately
- 🟡 **High** - Should fix soon, affects quality
- 🟢 **Medium** - Fix when convenient
- ⚪ **Low** - Nice to have, backlog

### When to Promote to Task File
If lingering item is:
- Taking >2 sessions to fix
- Requires significant new code (>200 lines)
- Affects multiple components
- Needs formal testing

→ Recommend: "This should become a proper task. Create task file?"

### Cleanup
When lingering task is DONE:
- Move from `🔥 Lingering` to `✅ Recent Completions`
- Archive session doc to `docs/archive/`
- Update PROJECT_STATUS