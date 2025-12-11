---
name: check-status
description: Quick context health check. Usage: /check-status
---

# Check Status

## 🚨 FIRST: Checkpoint Integrity

**Be honest - which applies?**

| Situation | Response |
|-----------|----------|
| Direct memory of this session | ✅ Continue |
| Started from checkpoint/summary | 🚨 **STOP** - Disclose, recommend fresh `/start-session` |
| Confused about state | 🔄 Run `/reload-context` |

**If checkpoint-only → HARD STOP.** Do not proceed.

---

## Quick Identity Check

| Question | Answer |
|----------|--------|
| **Developer?** | {Name} / ❓ Unknown |
| **Branch?** | {branch} / ❓ Unknown |
| **Working on?** | {task} / ❓ Unknown |

**If ANY ❓ → Run `/reload-context`**

---

## Status Report

```
📊 STATUS CHECK

👤 {Name} | 🌿 {branch}
📍 Context: {✅ Intact / ⚠️ Degrading / 🚨 Lost}

🎯 PRIMARY: {Phase N - Task}
   Status: {X}% | {✅/🚧/⏸️}

🔥 LINGERING ({count}):
   • {Issue 1} - {priority} {status}
   • {Issue 2} - {priority} {status}

📈 This Session:
   ✅ {completed 1}
   ✅ {completed 2}
   🚧 {in progress}

⏱️ Approx messages: {N}
💾 Context health: {OK / ⚠️ Wrap up / 🚨 New chat needed}
```

---

## Context Health Indicators

### Message Count (Approximate)
| Count | Status | Action |
|-------|--------|--------|
| 1-40 | ✅ Fresh | Continue freely |
| 40-60 | ⚠️ Aging | Plan wrap-up point |
| 60+ | 🚨 Risk | Complete current item, new chat |

### Degradation Symptoms
Watch for (in yourself):
- 🔄 Re-reading files already read
- 🔄 Asking answered questions
- 🔄 Repeating mistakes
- 🔄 Wrong file locations
- 🔄 User says "that's wrong"

**If symptoms present:**
```
⚠️ Showing degradation signs. Recommend:
- Save progress with /update-context
- Start fresh chat
```

---

## Task Completion Check

**Was a task just completed this session?**

| Answer | Action |
|--------|--------|
| Yes | → Suggest: "Task complete. Run `/update-context` to save progress?" |
| No | → Continue with status report |

---

## Quick Actions

| Situation | Command |
|-----------|---------|
| Everything OK | Continue working |
| Task just completed | `/update-context` |
| Minor confusion | `/reload-context` |
| Phase complete | `/phase-complete` |
| Need to save progress | `/update-context` |
| Things broken | `/abort` |
| Context exhausted | New chat + `/start-session` |
