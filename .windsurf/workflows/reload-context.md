---
name: reload-context
description: Emergency context recovery. Use when confused about state or after "summarizing conversation" appears.
auto_execution_mode: 0
---

# Reload Context

**Use when:**
- "Summarizing conversation" appeared
- Confused about task/branch/developer
- User says "you're confused"

---

## 1. Acknowledge Stale Context

Current in-memory context might be stale or hallucinated.
Discard assumptions and reload from disk.

---

## 2. Identify Developer

Check `.windsurf/team.md` for mapping.

Ask: **"Who are you?"**

---

## 3. Load Files

```
1. {dev_context_file}
2. PROJECT_STATUS.md
3. SOLUTION_ARCHITECTURE.md
```

```bash
git branch --show-current
git status --short
```

---

## 4. Extract Active Work

| Item | Value |
|------|-------|
| Primary task | {phase work} |
| Lingering | {bugs/ad-hoc} |
| Task Constants | {🔒 items} |

**If handoff exists:** Load `docs/tasks/{component}_phase{N}_handoff.md`

---

## 5. Confirm

```
🔄 CONTEXT RELOADED

👤 {name} | 🌿 {branch}
📄 {context_file}

🎯 PRIMARY: {task} Phase {N}
🔥 LINGERING: {count}
🔒 CONSTANTS: {count}

[P] Continue primary
[L] Lingering item
[?] Something else
```

---

## If Reload Fails

Context too degraded? **Start fresh:**
```
New chat → /start-session
```