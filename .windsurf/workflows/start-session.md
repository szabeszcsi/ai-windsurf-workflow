---
name: start-session
description: Initialize new chat session. Run at the start of every conversation.
auto_execution_mode: 0
---

# Start Session

Run this workflow at the beginning of every new chat.

---

## Step 1: Checkpoint Integrity

Before anything else, honestly assess:

| Situation | Action |
|-----------|--------|
| Direct memory of this session | ✅ Continue to Step 2 |
| Started from checkpoint/summary | 🚨 **DISCLOSE** → Tell user, recommend fresh start |
| Uncertain about state | Ask user to clarify |

**If checkpoint-only → STOP.** Do not pretend to have context you don't have.

---

## Step 2: Identify Developer

**Check if `.windsurf/team.md` exists:**

### Multi-developer project (team.md exists):

Ask:
```
🚨 WHO ARE YOU?
```

Then load their context file from the mapping:

| Developer | Context File |
|-----------|--------------|
| {Name 1} | dev1_context.md |
| {Name 2} | dev2_context.md |
| ... | ... |

### Single-developer project (no team.md):

Use `dev_context.md` directly.

---

## Step 3: Load Context

Read these files in order:

```
1. {dev_context_file}      → Current state, active task, Task Constants
2. PROJECT_STATUS.md       → Project overview (if exists)
3. SOLUTION_ARCHITECTURE.md → Project structure (if exists)
```

**If context file references external files (e.g., `docs/working/{task}_constants.md`), load those too.**

---

## Step 4: Verify Branch

```bash
git branch --show-current
git status --short
```

⚠️ Warn if branch doesn't match `dev_context.md`.

---

## Step 5: Present Work Options

Based on loaded context, show:

```
👤 {Name} | 🌿 {branch}

📋 AVAILABLE WORK:

🎯 PRIMARY: {Task Name} - Phase {N}
   Status: {X}% | Next: {next step}

🔥 LINGERING ({count}):
   1. {Issue} - {priority}
   2. {Issue} - {priority}

🆕 NEW: Describe a new task

Pick: [P] Primary | [1-N] Lingering | [N] New
```

---

## Step 6: Handle Selection

### PRIMARY selected:
1. Load handoff: `docs/tasks/{component}_phase{N}_handoff.md`
2. Review Task Constants (🔒 DO NOT MODIFY these)
3. Continue phase work

### LINGERING selected:
1. Load session doc from `docs/working/` if exists
2. Continue ad-hoc work

### NEW task:
Ask: *"Is this urgent (start now) or planned (create task file first)?"*

| Answer | Action |
|--------|--------|
| Urgent | Add to Lingering in dev_context, start immediately |
| Planned | Create task file using `.ai/templates/TASK_FILE_TEMPLATE.md` |

---

## Step 7: Confirm Ready

```
✅ SESSION READY

👤 Developer: {name}
🌿 Branch: {branch}
📋 Task: {selected work}
🔒 Constants: {count} items loaded

Ready to work!
```

---

## Quick Reference

| Situation | Action |
|-----------|--------|
| New chat | Run this workflow |
| Resuming after break | Run this workflow |
| Context feels stale | `/check-status` first |
| Phase just completed | `/phase-complete` then new chat |