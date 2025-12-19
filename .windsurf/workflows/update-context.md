---
name: update-context
description: Save progress mid-session. Use when you've made progress but phase isn't complete.
auto_execution_mode: 0
---

# Update Context

**Use when:** Made progress, session ending, switching tasks
**Don't use when:** Phase complete → use `/phase-complete`

---

## 1. Identify Developer

Check `.windsurf/team.md` for context file mapping.
Single-dev: `dev_context.md`

---

## 2. Classify Work

| Type | Action |
|------|--------|
| Primary phase | Update 🎯 section |
| Lingering task | Update 🔥 section |
| New issue | Add to 🔥 section |

---

## 3. Gather Summary

For each work item:
- What accomplished?
- Status (% complete, blocked)?
- Next step?

---

## 4. Check New Constants

Created anything future sessions must NOT break?
- Test scripts
- Key signatures
- Config structures

**If yes:** Add to 🔒 Task Constants

---

## 5. Update Context File

```markdown
## 🎯 Primary Task
**{Task}** - Phase {N} 🚧
- ✅ {done}
- 🚧 {in progress}
- [ ] {remaining}

Status: {X}%
Next: {step}
```

---

## 6. Size Check

**If context file > 2KB:**
- Archive old completed tasks to `docs/archive/`
- Keep only active work in context file

---

## 7. Confirm

```
✅ CONTEXT SAVED

Updated: {context_file}
Work: {type}
Status: {status}

Next session:
---
/start-session
Continue: {task}
---
```
