---
name: abort
description: Emergency abort and rollback. Usage: /abort
auto_execution_mode: 1
---

# Abort Workflow

Emergency recovery when things go wrong.

⚠️ **BEFORE EXECUTING THIS:** Tell the user what this will do, and ask for confirmation! Also tell the user what are the requirements for this workflow in order to successfully execute the steps!

---

## 🚨 STOP IMMEDIATELY

```
🚨 ABORT INITIATED - STOPPING ALL WORK
```

Do not make any more changes until recovery path is chosen.

---

## When to Use

- 🔥 Broke something and can't fix it
- 🔥 Tests failing after multiple attempts
- 🔥 Wrong branch, wrong files modified
- 🔥 Context severely degraded
- 🔥 Need to undo recent changes

---

## Step 1: Assess Damage

```bash
git status
git diff --stat
```

**Ask user:**
- What went wrong?
- How far back do we need to go?
- Are there uncommitted changes we want to keep?

---

## Step 2: Choose Recovery Path

### Option A: Discard Uncommitted Changes
```bash
git checkout -- .
git clean -fd
```
⚠️ **Destroys all uncommitted work**

### Option B: Stash Changes for Later
```bash
git stash push -m "Recovery stash {date}"
```
Saves current state, can retrieve later with `git stash pop`

### Option C: Restore from Backup (.bak files)
```bash
# If .bak files exist
ls *.bak
mv {file}.bak {file}
```
Restores from backup files if they were created

### Option D: Reset to Last Commit
```bash
git reset --hard HEAD
```
⚠️ **Destroys all changes since last commit**

### Option E: Reset to Specific Commit
```bash
git log --oneline -10
git reset --hard {commit-hash}
```
⚠️ **Destroys all changes since that commit**

### Option F: Selective Restore
```bash
# Restore specific file
git checkout HEAD -- path/to/file

# Restore specific directory
git checkout HEAD -- path/to/directory/
```

### Option G: Create Recovery Branch
```bash
git checkout -b recovery/{date}
```
Preserves current mess for later analysis, then switch back to main branch.

---

## Step 3: Verify Recovery

```bash
git status
git diff --stat

# Run tests if applicable
pytest tests/ -v --tb=short
```

---

## Step 4: Document Incident (Optional but Recommended)

Create `docs/working/incident_{date}.md`:

```markdown
# Incident {date}

## What Went Wrong
{description of the problem}

## Symptoms
- {symptom 1}
- {symptom 2}

## Recovery Action
{Option X: description}

## Root Cause
{if known}

## Prevention
{what to do differently next time}
```

---

## Step 5: Report

```
🔄 ABORT COMPLETE

Recovery: {action taken}
Status: {clean/needs more work}
Branch: {current branch}

Recommendation: Start fresh chat with /start-session
```

---

## Quick Recovery Commands

| Situation | Command |
|-----------|---------|
| Undo changes to one file | `git checkout -- {file}` |
| Undo all uncommitted changes | `git checkout -- .` |
| Remove untracked files | `git clean -fd` |
| Save work for later | `git stash` |
| Hard reset to last commit | `git reset --hard HEAD` |
| See recent commits | `git log --oneline -10` |
| See what changed | `git diff --stat` |
| Restore from backup | `mv {file}.bak {file}` |

---

## After Recovery

1. **Take a breath** - mistakes happen
2. **Start fresh chat** - degraded context likely contributed
3. **Review what went wrong** - learn from it
4. **Consider smaller steps** - commit more frequently
