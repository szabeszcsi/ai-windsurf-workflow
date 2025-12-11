# Start Session Workflow

Full protocol for initializing a new chat session.

---

## Step 1: Checkpoint Integrity Check (MANDATORY)

**Be honest with yourself:**

| Situation | Action |
|-----------|--------|
| Direct memory of this session | ✅ Continue to Step 2 |
| Started from checkpoint/summary | 🚨 **DISCLOSE TO USER** → Recommend fresh start |
| Uncertain about state | Ask user to clarify, recommend `/check-status` |

**If checkpoint-only → HARD STOP.** Tell user and recommend starting fresh.

---

## Step 2: Load Context

Read these files from project root:
1. `dev_context.md` - Current state, active task, lingering items
2. `SOLUTION_ARCHITECTURE.md` - Project structure

**If Task Constants section exists in dev_context.md:**
- These are SACRED - do not modify files/signatures listed there
- If it references an external file, load that too

---

## Step 3: Verify Branch

```bash
git branch --show-current
git status --short
```

Warn if branch doesn't match what's in `dev_context.md`.

---

## Step 4: Request Context Baseline

Ask user:
```
Please run `/context` and share the percentage so I can establish a baseline.
```

This helps track context health throughout the session.

---

## Step 5: Present Work Options

Show available work based on context:

```
👤 {Name} | 🌿 {branch}

📋 WHAT SHALL WE WORK ON?

🎯 PRIMARY: {Phase N - Task Name}
   └─ {brief status}

🔥 LINGERING ({count}):
   1. {Bug/Issue name} - {priority}
   2. {Investigation} - {priority}

🆕 NEW: Describe something else

Pick: [P=Primary] [1-N=Lingering] [N=New task]
```

---

## Step 6: Handle Selection

### If PRIMARY selected:
- Load handoff: `docs/tasks/{component}_phase{N}_handoff.md`
- Continue phase work

### If LINGERING selected:
- Load relevant session doc from `docs/working/`
- Continue ad-hoc work

### If NEW task:
- Ask: "Is this urgent (do now) or should we create a task file first?"
- **Urgent:** Add to Lingering in context, start work
- **Planned:** Create task file using template

---

## Step 7: Confirm Ready

```
✅ Session Ready

👤 Developer: {name}
🌿 Branch: {branch}
📋 Working on: {selected task}
📊 Context baseline: {X}%

🔒 Task Constants loaded:
   - {key item 1}
   - {key item 2}

Ready to go!
```

---

## Quick Examples

**Continue phase work:**
```
/start-session
→ Pick: P (Primary)
→ Load Phase N handoff, continue
```

**Fix a bug that came up:**
```
/start-session
→ Pick: 1 (Lingering - Excel generator bug)
→ Load bug context, fix it
```

**Something new and urgent:**
```
/start-session
→ Pick: N (New)
→ "Critical: Dashboard timeout"
→ Add to Lingering, start immediately
```
