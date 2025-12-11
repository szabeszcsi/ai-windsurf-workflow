# Developer Context

<!-- AI: Archive when >1.5KB. Update after each task. -->

**Name:** {Your Name}  
**Focus:** {Current primary task}  
**Updated:** {Date}

---

## 🌿 Branch
**Current:** `{branch-name}`  
**Status:** {Clean / Uncommitted changes / Ready to push}

---

## 🎯 Primary Task
**{Task Name}** - Phase {N} {✅/🚧/⏸️}
- Status: {X}% complete
- Current: {what you're doing now}
- Next: {immediate next step}
- Handoff: `docs/tasks/{component}_phase{N}_handoff.md`

---

## 🔒 Task Constants (DO NOT MODIFY)
<!-- 
Add items here as key decisions are made during the task.
These must NOT be modified in later phases without explicit permission.
Remove this section when the task is fully complete.
-->

**Task:** {Task Name} (Phases 1-{N})

| Item | Value | Established |
|------|-------|-------------|
| Test script | `{path}` | Phase {N} |
| Key signature | `{Class(params)}` | Phase {N} |
| Config key | `{key}` | Phase {N} |

---

## 🔥 Lingering Tasks
<!-- Quick bugs/issues to track. Promote to task file if >2 sessions to fix. -->

1. **{Issue name}** - {🔴/🟡/🟢} {✅/🚧}
   - {one-line description}
   - See: `docs/working/{issue}.md` (if exists)

---

## ✅ Recent Completions (Last 3)

1. ✅ {Completion 1} ({date})
2. ✅ {Completion 2} ({date})
3. ✅ {Completion 3} ({date})

---

## 📝 References

- Task: `docs/tasks/{task}_tasks.md`
- Architecture: `SOLUTION_ARCHITECTURE.md`
- Archive: `docs/archive/`

---

## 🚀 Next Session Prompt

```
I'm {Name}. {Brief context - what we're working on}.
Branch: {branch}
Primary: {task} Phase {N}
Read dev_context.md for current state.
```

---

<!-- 
SIZE GUIDELINES:
- Base context (without Task Constants): < 1.5 KB
- Task Constants section: < 500 bytes
- Total: < 2 KB

If Task Constants overflow, create docs/working/{task}_constants.md
and reference it here.

ARCHIVE TRIGGERS:
- Session > 2 days old → Archive to docs/archive/
- Context > 1.5 KB → Archive oldest sessions
- Phase complete → Move details to completion doc
- Task complete → Archive Task Constants, remove section
-->
