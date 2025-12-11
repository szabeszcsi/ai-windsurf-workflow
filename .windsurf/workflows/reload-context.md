---
name: reload-context
description: Emergency context recovery. Use when confused about state or after "summarizing conversation" appears.
auto_execution_mode: 0
---

# Reload Context

Emergency recovery when context is lost or confused.

**Use when:**
- 🚨 "Summarizing conversation" appeared
- ❓ Confused about task/branch/developer
- ❓ Made contradictory statements
- ⚠️ User says "you're confused"

---

## Step 1: Identify Developer

**Check `.windsurf/team.md` for developer mapping.**

Ask:
```
🚨 CONTEXT RECOVERY

Who are you?
```

| Developer | Context File |
|-----------|--------------|
| {from team.md} | {dev_context_file} |

**Single-developer project:** Use `dev_context.md`

---

## Step 2: Load Context Files

Read in order:

```
1. {dev_context_file}        → Developer state, Task Constants
2. PROJECT_STATUS.md         → Project overview
3. SOLUTION_ARCHITECTURE.md  → Project structure
```

```bash
git branch --show-current
git status --short
```

---

## Step 3: Identify Active Work

From context file, extract:

| Item | Value |
|------|-------|
| Primary task | {phase work in progress} |
| Lingering tasks | {bugs/ad-hoc items} |
| Current focus | {what was being worked on} |
| Task Constants | {🔒 items to preserve} |

**If active handoff exists:**
Load `docs/tasks/{component}_phase{N}_handoff.md`

---

## Step 4: Confirm Recovery

```
🔄 CONTEXT RELOADED

👤 Developer: {name}
🌿 Branch: {branch}
📄 Context: {dev_context_file}

🎯 PRIMARY: {task} - Phase {N}
🔥 LINGERING: {count} items
🔒 CONSTANTS: {count} items

Files loaded:
✅ {dev_context_file}
✅ PROJECT_STATUS.md
✅ {handoff if applicable}

What would you like to work on?
[P] Continue primary task
[L] Work on lingering item
[?] Something else
```

---

## If Reload Fails

Context too degraded to recover meaningfully?

**Start fresh:**
```
New chat → /start-session
```

Fresh context > degraded context.

---

## Quick Checklist

- [ ] Developer identified
- [ ] Context file loaded
- [ ] Branch verified
- [ ] Task Constants noted
- [ ] Active work identified
- [ ] Ready to continue