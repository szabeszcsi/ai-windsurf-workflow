---
name: start-session
description: Initialize session with task selection. Usage: /start-session [name]
---

# Start Session

## Step 1: Developer ID (MANDATORY)

**If name provided:** Use directly  
**If no name:**
```
🚨 WHO ARE YOU? Ferran or Szabi?
```

| Developer | Context | Primary Domain |
|-----------|---------|----------------|
| Ferran | `dev1_context.md` | SQL Layer |
| Szabi | `dev2_context.md` | Model/UI/Integration |

---

## Step 2: Load Context

Read from project root:
- `dev{X}_context.md` - **especially the 🔒 Task Constants section**
- `PROJECT_STATUS.md`

**If Task Constants references external file:**
- Also read `docs/working/{task}_constants.md`

**⚠️ Task Constants = DO NOT MODIFY** - these are decisions/files from earlier phases that must be preserved.

Template reference: `dev-context-template.md`

---

## Step 3: Verify Branch

```bash
git branch --show-current
git status --short
```

Warn if branch mismatch with context file.

---

## Step 4: Present Work Options

Show available work based on context:

```
👤 {Name} | 🌿 {branch}

📋 WHAT SHALL WE WORK ON?

🎯 PRIMARY: {Phase N - Task Name}
   └─ {brief status}

🔥 LINGERING ({count}):
   1. {Bug/Issue name} - {priority}
   2. {Investigation} - {priority}

📥 NEW: Describe something else

Pick: [1=Primary] [2-N=Lingering] [N=New task]
```

---

## Step 5: Handle Selection

### If PRIMARY selected:
- Load handoff: `docs/tasks/{layer}_phase{N}_handoff.md`
- Continue phase work

### If LINGERING selected:
- Load relevant session doc from `docs/working/`
- Continue ad-hoc work

### If NEW task:
- Ask: "Is this urgent (do now) or should we create a task file first?"
- **Urgent:** Add to Lingering in context, start work
- **Planned:** Offer to run task generation (see TASK_FILE_GENERATION_GUIDE.md)

---

## Step 6: Confirm Ready

```
✅ Session Ready

👤 Developer: {name}
🌿 Branch: {branch}
📋 Working on: {selected task}
📍 Type: {Primary Phase / Lingering / New}

🔒 Task Constants loaded:
   - Test: {test script path}
   - Preserve: {key items}

Context loaded. Ready to go!
```

---

## Quick Examples

**Continue phase work:**
```
/start-session Szabi
→ Pick: 1 (Primary)
→ Load Phase N handoff, continue
```

**Fix a bug that came up:**
```
/start-session Szabi
→ Pick: 2 (Lingering - Excel generator bug)
→ Load bug context, fix it
```

**Something new and urgent:**
```
/start-session Szabi
→ Pick: N (New)
→ "Critical: Dashboard timeout"
→ Add to Lingering, start immediately
```
