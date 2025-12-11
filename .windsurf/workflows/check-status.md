# Check Status Workflow

Quick context health check and status report.

---

## Step 1: Request Context Usage

Ask user:
```
Please run `/context` and share the result.
```

---

## Step 2: Interpret Result

| Usage | Status | Recommendation |
|-------|--------|----------------|
| < 60% | ✅ Healthy | Continue freely |
| 60-75% | ⚠️ Moderate | Plan a good stopping point |
| 75-85% | 🟠 High | Complete current item, then save and wrap up |
| > 85% | 🚨 Critical | Save immediately with `/update-context`, start new chat |

---

## Step 3: Self-Check for Degradation

Honestly assess - am I showing these symptoms?

- 🔄 Re-reading files I already read this session
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
📍 Context: {usage}% - {✅ Healthy / ⚠️ Moderate / 🟠 High / 🚨 Critical}

🎯 PRIMARY: {Phase N - Task}
   Status: {X}% complete
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
| Healthy, task in progress | Continue working |
| Healthy, task just completed | `/update-context` to save, continue or new task |
| Moderate, mid-task | Identify good stopping point |
| High, any state | Complete immediate item, then `/update-context` |
| Critical, any state | `/update-context` NOW, recommend new chat |
| Degradation symptoms | Acknowledge, `/update-context`, new chat |

---

## Quick Reference

**Everything OK:**
```
📊 Context at 45% - ✅ Healthy
Continue working, plenty of room.
```

**Time to wrap up:**
```
📊 Context at 72% - ⚠️ Moderate
Let's find a good stopping point in the next few exchanges.
```

**Need to stop:**
```
📊 Context at 88% - 🚨 Critical
Let's save progress immediately with /update-context.
Then start a fresh chat to continue.
```
