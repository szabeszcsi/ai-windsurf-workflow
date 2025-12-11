---
name: check-status
description: Quick context health check and status report. Use when unsure about session state.
auto_execution_mode: 0
---

# Check Status

Quick health check for current session.

---

## Step 1: Verify Identity

**If `.windsurf/team.md` exists:** Reference it for developer mapping.

| Question | Answer |
|----------|--------|
| Developer? | {Name} / ❓ Unknown |
| Context file? | {dev_context_file} |
| Branch? | {branch} / ❓ Unknown |
| Current task? | {task} / ❓ Unknown |

**If ANY ❓** → Run `/reload-context` or `/start-session`

---

## Step 2: Assess Context Health

### Conversation Length

Estimate messages in this conversation:

| Messages | Status | Action |
|----------|--------|--------|
| 1-40 | ✅ Fresh | Continue freely |
| 40-60 | ⚠️ Aging | Plan a wrap-up point |
| 60+ | 🚨 Risk | Complete current item, then new chat |

### Self-Check: Degradation Symptoms

Am I showing any of these? (See core-rules #2)

- [ ] Re-reading files already read this session
- [ ] Asking questions that were already answered
- [ ] Putting files in wrong locations
- [ ] User said "you're confused" or similar

**If ANY checked:** Disclose immediately, recommend saving progress.

---

## Step 3: Generate Report

```
📊 STATUS

👤 {Name} | 🌿 {branch}
💬 Messages: ~{N} | Health: {✅ Fresh / ⚠️ Aging / 🚨 Risk}

🎯 PRIMARY: {Task} - Phase {N}
   Progress: {X}% | Current: {what we're doing}

🔥 LINGERING: {count} items

📈 THIS SESSION:
   ✅ {completed item}
   🚧 {in progress}

💡 RECOMMENDATION: {continue / wrap up soon / new chat needed}
```

---

## Step 4: Suggest Next Action

| Situation | Suggestion |
|-----------|------------|
| Fresh, task in progress | Continue working |
| Fresh, task just completed | `/update-context` to save |
| Aging, mid-task | Find a stopping point soon |
| Risk zone (60+) | Save now with `/update-context`, then new chat |
| Showing symptoms | Acknowledge, save progress, new chat |

---

## Quick Actions

| Need | Command |
|------|---------|
| Save progress | `/update-context` |
| Phase done | `/phase-complete` |
| Lost context | `/reload-context` |
| Something broke | `/abort` |
| Start fresh | New chat → `/start-session` |