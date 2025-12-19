---
name: start-session
description: Initialize new chat session. Run at the start of every conversation.
auto_execution_mode: 0
---

# Workflow: Start Session

1. **Checkpoint Check**
   - **Direct Memory:** Continue.
   - **Checkpoint/Summary:** 🚨 DISCLOSE -> Recommend `/start-session` (fresh start).
   - **Uncertain:** Ask user.

2. **Identity & Environment**
   - **Developer:** Check `.windsurf/team.md`. Ask "Who are you?" -> Load `dev{N}_context.md`.
   - **Branch:** `git branch --show-current`
   - **Python:** `python --version` (Verify venv is active).

3. **Context Recovery**
   - Read loaded context file.
   - Read `PROJECT_STATUS.md` (if exists).
   - Summarize: "Active Phase: [Phase]. Last Status: [Status]."
   
4. **Present options**

```
👤 {Name} | 🌿 {branch}

📋 WORK OPTIONS:

🎯 PRIMARY: {Task} - Phase {N}
   Status: {X}% | Next: {step}

🔥 LINGERING: {count} items

🆕 NEW: Describe new task

[P] Primary | [1-N] Lingering | [N] New
```

5. **Work Selection**
   - **Primary:** Resume active task (Load handoff `docs/tasks/{component}_phase{N}_handoff.md` if phase start).
   - **Lingering:** Pick up saved session from `docs/working/`.
   - **New:** Describe new task.

6. **Ready**
   - "Session Ready. User: [Name]. Branch: [Branch]. Awaiting instructions."
