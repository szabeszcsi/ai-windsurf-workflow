---
trigger: always_on
---

# Core Rules

## 0. CHECKPOINT INTEGRITY

**On FIRST interaction or `/check-status`:**

| Situation | Action |
|-----------|--------|
| Direct memory of this session | ✅ Continue |
| Started from checkpoint/summary | 🚨 **DISCLOSE** → Recommend `/start-session` |
| Confused about state | 🔄 `/reload-context` |

**Never pretend to have direct memory when you don't.**

---

## 1. SESSION START

Every new chat: **Run `/start-session`**

Multi-developer teams: See `.windsurf/team.md` for developer → context file mapping.

---

## 2. CONTEXT DEGRADATION

**Self-monitor for these symptoms:**
- Re-reading files already read this session
- Asking answered questions
- Creating files in wrong locations
- User says "you're confused"

**If detected:** Disclose immediately, recommend `/check-status` or new chat.

---

## 3. CODE EDITING SAFETY

- **Before multi-file edits:** Create `.bak` backups
- **After 3+ failed attempts:** Restore from backup, reassess approach

---

## 4. FILE PLACEMENT

| Type | Location |
|------|----------|
| Source code | `src/{module}/` |
| Unit tests | `tests/unit/` |
| Integration tests | `tests/integration/` |
| Test utilities | `tests/utilities/` |
| Scripts | `scripts/` |
| Task docs | `docs/tasks/` |
| Working docs | `docs/working/` |
| Archives | `docs/archive/` |

**Never in project root** except: main entry point, README, config files, dev_context.md

---

## 5. ENVIRONMENT

Before running tests, verify virtual environment:
```bash
which python  # Unix
where python  # Windows
```

---

## 📂 Load On Demand

| When | Read/Run |
|------|----------|
| Starting task | `docs/tasks/{component}_phase{N}_handoff.md` |
| Writing Python | `.ai/standards/python.md` |
| Writing tests | `.ai/standards/testing.md` |
| Creating handoff | `.ai/templates/HANDOFF_TEMPLATE.md` |
| Saving progress | Run `/update-context` |
| Phase complete | Run `/phase-complete` |
| Context confused | Run `/reload-context` |
| System unclear | `.ai/AGENT_REFERENCE.md` |
| Emergency | Run `/abort` |