# Session Archive Template

## Purpose
**This template is for AI assistants to follow when archiving developer context files.**

## When AI Should Archive (Automatically)
1. **Size trigger:** When dev context file exceeds 1.5KB
2. **Age trigger:** Sessions older than 2 days
3. **Manual trigger:** When developer says "archive old sessions"
4. **Session end:** At end of work day

## Archive File Location
- Save to: `docs/archive/dev[1/2]_sessions_[YYYY-MM].md`
- Template location: `docs/session_archive_template.md` (this file)

---

## Archive File Naming Convention

```
docs/archive/
├── dev1_sessions_2025-11.md    # Ferran's November 2025 sessions
├── dev2_sessions_2025-11.md    # Szabi's November 2025 sessions
├── context_health_2025.md      # Yearly context health archive
└── decisions_2025-Q4.md        # Major decisions archive
```

---

## Archive Format

```markdown
# Dev[X] Session Archive - [YYYY-MM]

## Summary Stats
- **Total Sessions:** [count]
- **Major Features Completed:** [list]
- **Key Decisions Made:** [list]

## Archived Sessions

### [Date] - [Feature/Task Name]
**Branch:** [branch name]
**Files Modified:** [count]
**Outcome:** [1-2 lines]
**Key Learning:** [if any]
**Linked PR:** [if applicable]

### [Older Date] - [Feature/Task Name]
...
```

---

## Example Archive Entry

```markdown
# Dev2 Session Archive - 2024-11

## Summary Stats
- **Total Sessions:** 12
- **Major Features Completed:** Model Layer XMLA connection, UI Parser prototype
- **Key Decisions Made:** Use pyadomd for XMLA, Separate extraction from enhancement

## Archived Sessions

### 2024-11-20 - Model Layer XMLA Connection
**Branch:** feature/model-layer-xmla
**Files Modified:** 5
**Outcome:** Successfully connected to Power BI service via XMLA endpoint
**Key Learning:** Must use pyadomd for stability, not raw XMLA
**Linked PR:** #23

### 2024-11-18 - UI Parser Initial Design
**Branch:** feature/ui-parser
**Files Modified:** 3
**Outcome:** Created PBIR parser that extracts visuals and pages
**Key Learning:** Report.json structure is nested differently than expected
```

---

## What to Archive (AI moves to archive)

### I MUST Archive:
- ✅ Sessions older than 2 days
- ✅ Completed feature work (keep 1-line summary in context)
- ✅ Resolved blockers
- ✅ Old TODO items (completed or cancelled)
- ✅ Detailed explanations (compress to 1 line)
- ✅ Any session that caused context overflow

### I MUST Keep (in active context):
- ❌ Current task and branch
- ❌ Today's work + yesterday's brief summary
- ❌ Active blockers
- ❌ Prototype file locations (always needed)
- ❌ Decisions affecting current work
- ❌ Last 2-3 task completions (1 line each)

---

## Archive Process (AI Steps)

### Before Archiving:
- [ ] Check current dev context file size
- [ ] Identify sessions older than 2 days
- [ ] Note current task and branch to preserve

### During Archive:
- [ ] Read this template for correct format
- [ ] Copy old sessions to `docs/archive/dev[X]_sessions_[YYYY-MM].md`
- [ ] Compress each session to 2-3 lines
- [ ] Remove code blocks (they should be in prototype files)
- [ ] Keep only decision outcomes and completions

### After Archive:
- [ ] Update dev context with: "📁 Archived X sessions to docs/archive/dev[X]_sessions_[date].md"
- [ ] Verify dev context now < 1.5KB
- [ ] Update context_health.md with archive action
- [ ] Confirm to developer: "Archive complete, context reduced from XKB to YKB"

---

## AI Archive Implementation

When archiving, I will:
1. Create archive file if it doesn't exist
2. Append compressed sessions with date headers
3. Keep format consistent with this template
4. Preserve only essential information

**Example AI Archive Action:**
```
"I'm archiving sessions older than 2 days:
- Reading docs/session_archive_template.md
- Moving 3 old sessions to docs/archive/dev2_sessions_2024-11.md
- Compressed from 2.1KB to 0.8KB
- Current context now shows only active work
Archive complete!"
```

---

## Compression Guidelines

### Verbose (remove):
```markdown
### Session: Working on Model Layer
Today I started working on the model layer. First, I reviewed the old code
in modelDocumenter to understand how it worked. Then I created a new file
for the XMLA connector. I had some issues with authentication but figured
out we need to use pyadomd. After testing several approaches...
```

### Compressed (keep):
```markdown
### 2024-11-20 - Model Layer XMLA
✅ Created XMLA connector using pyadomd
🔧 Next: Add measure extraction
```

---

## Search Archive Command

When you need to find old decisions:
```bash
# Search all archives for keyword
grep -r "XMLA" docs/archive/

# Find specific month's work
cat docs/archive/dev2_sessions_2024-11.md | grep -A 2 "2024-11-20"
```

---

## Red Flags - Archive Immediately If:

1. 🚨 Dev context file > 2KB (should be <1.5KB ideally)
2. 🚨 Same information repeated 2+ times
3. 🚨 Code blocks in markdown (move to prototype files NOW)
4. 🚨 Sessions older than 2 days
5. 🚨 "Summarizing conversation history" appeared even once
6. 🚨 More than 5 completed tasks listed (keep only last 3)

---

**Template Version:** 1.1
**Created:** 2024-11-24
**Updated:** 2025-11-26
**Purpose:** Maintain lean context files to prevent token overflow