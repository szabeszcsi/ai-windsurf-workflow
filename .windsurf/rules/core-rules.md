---
trigger: always_on
---

# 🚨 HARD STOPS

## 0. CHECKPOINT INTEGRITY (HIGHEST PRIORITY)

**On FIRST interaction or any `/check-status`:**

| Situation | Action |
|-----------|--------|
| Direct memory of this session | ✅ Continue normally |
| Started from checkpoint/summary | 🚨 **DISCLOSE IMMEDIATELY** → Recommend fresh `/start-session` |
| Confused about state | 🔄 Run `/reload-context` |

**NEVER pretend to have direct memory when you don't.**

---

## 1. SESSION START

```
🚨 WHO ARE YOU? (e.g., Ferran, Szabi, or your developer ID)
```

**NO EXCEPTIONS.** Then read `./dev{X}_context.md` and verify branch.

**Pattern:** `dev{X}_context.md` where X = developer number

| Developer | Context File |
|-----------|--------------|
| Ferran | `./dev1_context.md` |
| Szabi | `./dev2_context.md` |

*(Example - customize for your team)*

---

## 2. TESTS PASS → PHASE COMPLETE

When tests pass and phase work done:
```
🚨 STOP - Run `/phase-complete` before committing.
```

---

## 3. CONTEXT DEGRADATION

**Symptoms (self-monitor continuously):**
- Re-reading files already read this session
- Asking answered questions / repeating mistakes
- Creating files in wrong locations
- User says "you seem confused"

**If ANY detected:**
```
⚠️ Context degradation detected. Recommend `/check-status` or fresh chat.
```

---

## 4. CONTEXT FILE SIZE

**Size limits for dev{X}_context.md:**

| Component | Limit |
|-----------|-------|
| Base context (without constants) | < 1.5 KB |
| 🔒 Task Constants | < 500 bytes |
| **Total** | < 2 KB |

**If Task Constants overflow (>500 bytes):**
1. Create `docs/working/{task}_constants.md` with full details
2. Keep summary in context file, reference the external file
3. Load external file at session start

**When PRIMARY task completes:**
1. Archive Task Constants to completion doc
2. Remove 🔒 section from context (or replace with new task's constants)
3. Context should drop back to <1.5 KB

---

## 4. CODE EDITING SAFETY

- **Before multi-file edits:** Create `.bak` backups
- **After 3+ failed attempts:** Restore from backup
- **When working:** Delete `.bak` files

---

## 5. FILE PLACEMENT

| Type | Location |
|------|----------|
| Tests | `tests/unit/`, `tests/integration/` |
| Test utilities | `tests/utilities/` |
| Scripts | `scripts/` |
| Source | `src/{module}/` (e.g., backend/, api/, frontend/) |
| Task docs | `docs/tasks/` |
| Archives | `docs/archive/` |
| Temp files | `docs/working/` |

**NEVER:** project root (except main.py, README, PROJECT_STATUS, dev_context)

---

## 6. PLANNING & CODE HYGIENE

- **Plan before coding** - brief steps, confirm with user
- **No code in chat** - create files, show only <10 line snippets
- **Context file limit:** >2KB → archive immediately
- **🔒 Task Constants are SACRED** - never modify files/signatures listed there without explicit permission

---

## 7. ENVIRONMENT

**Verify correct virtual environment activated before running tests.**

```bash
python --version  # Check Python version
# Activate venv if needed (adjust path for your project)
```

---

## 📂 Load On Demand

| When | Read |
|------|------|
| Starting task | `docs/tasks/{layer}_phase{N}_handoff.md` |
| Writing code | `.github/copilot-instructions.md` |
| Creating handoff | `docs/ai/TEMPLATES/HANDOFF_DOC_TEMPLATE.md` |
| Emergency | `/abort` |
