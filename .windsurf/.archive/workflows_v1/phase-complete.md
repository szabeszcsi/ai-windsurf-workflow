---
description: Phase completion protocol. Usage: /phase-complete
auto_execution_mode: 1
---

# Phase Complete

## 🚨 HARD STOP
```
🚨 STOP - PHASE COMPLETE - CANNOT COMMIT YET
```

---

## Pre-Check

**Before proceeding, confirm:**
1. Am I working from direct session memory? (If checkpoint-only → STOP, disclose to user)
2. Tests passing?
3. On correct feature branch?

---

## Steps (All Required)

| # | Action | Output |
|---|--------|--------|
| 1 | Gather info | Layer, phase #, developer, description |
| 2 | Run tests | `pytest tests/unit/ -v` → must pass |
| 3 | Verify branch | `git branch --show-current` |
| 4 | Create completion doc | `docs/tasks/{layer}_phase{N}_complete.md` |
| 5 | **Create handoff** 🚨 | `docs/tasks/{layer}_phase{N+1}_handoff.md` |
| 6 | Update dev context | `dev{X}_context.md` (preserve 🔒 Task Constants!) |
| 7 | Update PROJECT_STATUS | Active Work + Recent Changes |
| 8 | Update PROJECT_DETAILS | Change History section |
| 9 | Archive old handoff | Move to `docs/tasks/completed/` |
| 10 | Git commit & push | Only after steps 4-9 |
| 11 | Final report | Provide new chat prompt |

**Step 6 Note:** Keep `🔒 Task Constants` unless this is the FINAL phase. Include constants in handoff doc too.

**For templates and code blocks → read `docs/ai/templates/phase-complete-templates.md`**

---

## Checklist (All Must Be ✅)

- [ ] Tests passing
- [ ] Completion doc created
- [ ] **Handoff doc created** ← Most forgotten! (skip if final phase)
- [ ] Dev context updated
- [ ] **🔒 Task Constants preserved** ← Or archived if final phase
- [ ] PROJECT_STATUS.md updated
- [ ] PROJECT_DETAILS.md updated
- [ ] Old handoff archived
- [ ] Git committed and pushed
- [ ] New chat prompt provided

---

## Final Phase Special Handling

**If this is the LAST phase of a task:**

1. **No handoff doc needed** (no next phase)
2. **Archive Task Constants** to completion doc:
   ```markdown
   ## 🔒 Task Constants (Archived)
   These were the key invariants for this task:
   {copy from dev context}
   ```
3. **Remove 🔒 section** from dev context (task complete)
4. **Context file should shrink** back to <1.5 KB

---

## Final Output

```
🎉 Phase {N} Complete!

✅ Created: docs/tasks/{layer}_phase{N}_complete.md
✅ Created: docs/tasks/{layer}_phase{N+1}_handoff.md
✅ Updated: dev{X}_context.md
✅ Updated: PROJECT_STATUS.md
✅ Updated: PROJECT_DETAILS.md
✅ Committed and pushed

⚠️ START PHASE {N+1} IN A NEW CHAT
```