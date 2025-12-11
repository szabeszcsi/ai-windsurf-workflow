# Phase Failed / Abandoned Workflow

Protocol for handling phases that cannot be completed as planned.

**Use this when:** Phase is blocked, abandoned, or needs restart (NOT for emergencies - use `/abort` for that).

---

## When to Use This (vs /abort)

| Situation | Use |
|-----------|-----|
| Broke something, need to undo | `/abort` |
| External dependency blocking | **This workflow** |
| Requirements changed mid-phase | **This workflow** |
| Approach proved unworkable | **This workflow** |
| User wants to abandon phase | **This workflow** |
| Too complex, needs redesign | **This workflow** |
| Context degraded, confused | `/abort` then new session |

---

## Step 1: Document Current State

Before anything else, capture what exists:

```bash
git status
git diff --stat
```

**Create failure doc:** `docs/tasks/{component}_phase{N}_failed.md`

```markdown
# {Component} Phase {N} - Failed/Abandoned

**Date:** {date}
**Developer:** {name}
**Branch:** `{branch}`

## Status at Failure
- Started: {date}
- Ended: {date}
- Progress: {X}% complete

## What Was Attempted
{Brief description of approach and what was built}

## Files Created/Modified
| File | Status | Notes |
|------|--------|-------|
| `{path}` | Keep/Delete/Incomplete | {why} |

## Reason for Failure
{One of:}
- [ ] External blocker: {description}
- [ ] Requirements changed: {what changed}
- [ ] Technical: approach didn't work
- [ ] Complexity: needs redesign
- [ ] User decision: abandon feature

## What We Learned
- {Lesson 1}
- {Lesson 2}

## Recommendations
{What to do differently if attempting again}
```

---

## Step 2: Choose Path Forward

### Option A: Restart Phase (Different Approach)

1. Keep failure doc for reference
2. Discard or stash incomplete work:
   ```bash
   git stash push -m "Phase {N} failed attempt"
   ```
3. Create new handoff doc for retry:
   ```markdown
   # {Component} Phase {N} Retry Handoff

   **Previous attempt:** See docs/tasks/{component}_phase{N}_failed.md
   **What went wrong:** {summary}
   **New approach:** {description}
   ```
4. Update dev_context.md with new approach

### Option B: Skip Phase (Move to Next)

1. Keep failure doc
2. Commit partial work if useful:
   ```bash
   git add .
   git commit -m "WIP: Phase {N} partial (abandoned)"
   ```
3. Create handoff for Phase {N+1}
4. Note in handoff what was skipped and why

### Option C: Abandon Feature Entirely

1. Keep failure doc for future reference
2. Remove incomplete work:
   ```bash
   git checkout -- .
   git clean -fd
   ```
3. Update dev_context.md:
   - Remove primary task
   - Add to "Abandoned" or archive

### Option D: Wait for Blocker Resolution

1. Commit work-in-progress:
   ```bash
   git add .
   git commit -m "WIP: Phase {N} blocked on {blocker}"
   ```
2. Update dev_context.md:
   ```markdown
   ## Primary Task
   **{Task}** - Phase {N} ⏸️ BLOCKED
   - Blocker: {description}
   - Waiting for: {what needs to happen}
   - Resume when: {condition}
   ```
3. Start different work on separate branch

---

## Step 3: Update dev_context.md

**For restart (Option A):**
```markdown
## Primary Task
**{Task}** - Phase {N} 🔄 RETRY
- Previous attempt failed: docs/tasks/{component}_phase{N}_failed.md
- New approach: {brief description}
```

**For skip (Option B):**
```markdown
## Primary Task
**{Task}** - Phase {N+1} 🚧
- Note: Phase {N} skipped (see failed doc)
```

**For abandon (Option C):**
```markdown
## Abandoned Tasks
- {Task}: {brief reason} (docs/tasks/{component}_phase{N}_failed.md)
```

**For blocked (Option D):**
```markdown
## Primary Task
**{Task}** - Phase {N} ⏸️ BLOCKED
- Blocker: {description}
- ETA: {if known}
```

---

## Step 4: Handle Task Constants

**If restarting:** Keep Task Constants (they're still valid)

**If abandoning:** Archive to failure doc, remove from dev_context.md:
```markdown
## Archived Task Constants
These were established before abandonment:
{copy constants here}
```

**If changing approach significantly:** Review constants - some may no longer apply

---

## Checklist

- [ ] Failure doc created
- [ ] Current work handled (stash/commit/discard)
- [ ] dev_context.md updated
- [ ] Task Constants handled appropriately
- [ ] Path forward chosen and documented
- [ ] New session prompt provided (if needed)

---

## Final Output

```
⚠️ Phase {N} Failed/Abandoned

Status: {Restart / Skip / Abandon / Blocked}
Doc: docs/tasks/{component}_phase{N}_failed.md
Work: {Stashed / Committed WIP / Discarded}

Next action: {description}

{If new session needed:}
---
I'm {name}. {Task} Phase {N} failed.
Read docs/tasks/{component}_phase{N}_failed.md for context.
New approach: {brief}
Branch: {branch}
---
```

---

## Quick Reference

| Status | Icon | Meaning |
|--------|------|---------|
| In Progress | 🚧 | Actively working |
| Complete | ✅ | Done, committed |
| Blocked | ⏸️ | Waiting on external |
| Retry | 🔄 | Restarting with new approach |
| Failed | ❌ | Abandoned |
