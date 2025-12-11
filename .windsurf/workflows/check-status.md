---
name: check-status
description: Quick context health check and status report. Usage: /check-status
auto_execution_mode: 0
---

# Check Status Workflow

Quick context health check and status report.

---

## Step 1: Checkpoint Integrity Check (CRITICAL)

**Be honest - which applies?**

| Situation | Response |
|-----------|----------|
| Direct memory of this session | ✅ Continue to Step 2 |
| Started from checkpoint/summary | 🚨 **STOP** - Disclose, recommend fresh `/start-session` |
| Confused about state | 🔄 Run `/reload-context` |

**If checkpoint-only → HARD STOP.** Disclose to user immediately.

---

## Step 2: Identity Check

| Question | Answer |
|----------|--------|
| **Developer?** | {Name} / ❓ Unknown |
| **Branch?** | {branch} / ❓ Unknown |
| **Working on?** | {task} / ❓ Unknown |

**If ANY ❓ → Run `/reload-context`**

---

## Step 3: Assess Context Health

### Message Count (Approximate)

Estimate how many messages in this conversation:

| Count | Status | Action |
|-------|--------|--------|
| 1-40 | ✅ Fresh | Continue freely |
| 40-60 | ⚠️ Aging | Plan wrap-up point |
| 60+ | 🚨 Risk | Complete current item, new chat |

### Degradation Symptoms

Honestly assess - am I showing these symptoms?

- 🔄 Re-reading files already read this session
- 🔄 Asking questions that were already answered
- 🔄 Repeating mistakes I made earlier
- 🔄 Putting files in wrong locations
- 🔄 Confused about what we're working on
- 🔄 User has said "that's wrong" or "you're confused"

**If ANY symptoms present:**
```
⚠️ I'm showing signs of context degradation.
Recommend: Save progress now with /update-context and start fresh chat.
```

---

## Step 4: Generate Status Report

```
📊 STATUS CHECK

👤 {Name} | 🌿 {branch}
📍 Context: {✅ Intact / ⚠️ Degrading / 🚨 Lost}
⏱️ Messages: ~{N} ({✅ Fresh / ⚠️ Aging / 🚨 Risk})

🎯 PRIMARY: {Phase N - Task}
   Status: {X}% complete | {✅/🚧/⏸️}
   Current: {what we're doing now}

🔥 LINGERING ({count}):
   • {Issue 1} - {priority} {status}
   • {Issue 2} - {priority} {status}

📈 This Session:
   ✅ {completed item 1}
   ✅ {completed item 2}
   🚧 {in progress}

💡 Recommendation: {continue / wrap up soon / save and new chat}
```

---

## Step 5: Provide Guidance

Based on status, suggest next action:

| Situation | Suggestion |
|-----------|------------|
| Fresh context, task in progress | Continue working |
| Fresh context, task just completed | `/update-context` to save, continue or new task |
| Aging context, mid-task | Identify good stopping point |
| High message count, any state | Complete immediate item, then `/update-context` |
| Risk zone (60+ messages) | `/update-context` NOW, recommend new chat |
| Degradation symptoms | Acknowledge, `/update-context`, new chat |

---

## Quick Reference

**Everything OK:**
```
📊 Context: ✅ Fresh (25 messages)
Continue working, plenty of room.
```

**Time to wrap up:**
```
📊 Context: ⚠️ Aging (48 messages)
Let's find a good stopping point in the next few exchanges.
```

**Need to stop:**
```
📊 Context: 🚨 Risk (65 messages)
Let's save progress immediately with /update-context.
Then start a fresh chat to continue.
```

---

## Task Completion Check

**Was a task just completed this session?**

| Answer | Action |
|--------|--------|
| Yes | → Suggest: "Task complete. Run `/update-context` to save progress?" |
| No | → Continue with current work |

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
