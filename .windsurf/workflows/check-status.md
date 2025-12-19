---
name: check-status
description: Quick context health check and status report. Use when unsure about session state.
auto_execution_mode: 0
---

# Check Status

## 1. Verify Identity

| Item | Value |
|------|-------|
| Developer | {name} / ❓ |
| Context file | {file} |
| Branch | {branch} / ❓ |
| Task | {task} / ❓ |

**If any ❓:** Run `/reload-context` or `/start-session`

---

## 2. Session Health

**Message count estimate:**

| Count | Status | Action |
|-------|--------|--------|
| 1-40 | ✅ Fresh | Continue |
| 40-60 | ⚠️ Aging | Plan wrap-up |
| 60+ | 🚨 Risk | Complete current, new chat |

**Degradation symptoms:**
- Re-reading files already read
- Asking answered questions
- Wrong file locations

---

## 3. Context Sync Check

Does `dev_context.md` match reality?
- Current task accurate?
- Phase number correct?
- Task Constants up to date?

**If desynced:** Update context file or run `/reload-context`

---

## 4. Report

```
📊 STATUS

👤 {Name} | 🌿 {branch}
💬 ~{N} messages | {health}

🎯 PRIMARY: {Task} Phase {N}
   {X}% | Current: {work}

🔥 LINGERING: {count}

📈 THIS SESSION:
   ✅ {completed}
   🚧 {in progress}

💾 Context: {Synced/Desynced}
💡 {recommendation}
```

---

## 5. Next Action

| Situation | Suggestion |
|-----------|------------|
| Fresh, working | Continue |
| Fresh, task done | `/update-context` |
| Aging, mid-task | Find stopping point |
| Risk zone | Save now, new chat |
| Desynced | `/reload-context` |
