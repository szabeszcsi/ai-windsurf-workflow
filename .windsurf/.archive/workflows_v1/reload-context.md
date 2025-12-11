---
name: reload-context
description: Emergency context recovery. Usage: /reload-context
---

# Reload Context

## When to Use

- 🚨 "Summarizing conversation" appeared
- ❓ Confused about task/branch/developer
- ❓ Made contradictory statements
- ⚠️ User says "you're confused"

---

## Step 1: Ask Developer

```
🚨 CONTEXT RECOVERY

Who are you? (Ferran / Szabi)
```

Wait for answer.

---

## Step 2: Load Files

```bash
# Read in order:
1. dev{X}_context.md      # Developer state
2. PROJECT_STATUS.md       # Project overview
3. git branch --show-current
4. git status --short
```

---

## Step 3: Identify Active Work

From context file, extract:
- **Primary task:** Phase work in progress
- **Lingering tasks:** Bugs/ad-hoc items
- **Current focus:** What was being worked on

If active handoff exists:
- Read `docs/tasks/{layer}_phase{N}_handoff.md`

---

## Step 4: Confirm Recovery

```
🔄 CONTEXT RELOADED

👤 Developer: {name}
🌿 Branch: {branch}

🎯 Primary: {task} - Phase {N}
🔥 Lingering: {count} items

Files loaded:
✅ dev{X}_context.md
✅ PROJECT_STATUS.md
✅ {handoff if applicable}

What would you like to work on?
[P] Continue primary task
[L] Work on lingering item
[?] Something else
```

---

## If Reload Fails

Start **new chat** with:
```
/start-session {name}
```

Fresh context > degraded context.

---

## Quick Recovery Checklist

- [ ] Developer identified
- [ ] Context file read
- [ ] Branch verified
- [ ] Active work identified
- [ ] Ready to continue
