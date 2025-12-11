---
description: Emergency abort and rollback. Usage: /abort
auto_execution_mode: 1
---

# 🚨 ABORT

Emergency recovery when things go wrong.
BEFORE EXECUTING THIS: Tell the user what this will do, and ask for confirmation! Also tell the user what are the requirements for this workflow in order to sucessfully execute the steps!

---

## When to Use

- 🔥 Broke something and can't fix it
- 🔥 Tests failing after multiple attempts
- 🔥 Wrong branch, wrong files modified
- 🔥 Context severely degraded
- 🔥 Need to undo recent changes

---

## Step 1: STOP

```
🚨 ABORT INITIATED - STOPPING ALL WORK
```

Do not make any more changes.

---

## Step 2: Assess Damage

```bash
git status
git diff --stat
```

**Ask user:**
- What went wrong?
- How far back do we need to go?

---

## Step 3: Choose Recovery Path

### Option A: Discard Uncommitted Changes
```bash
git checkout -- .
git clean -fd
```
⚠️ **Destroys all uncommitted work**

### Option B: Restore from Backup
```bash
# If .bak files exist
ls *.bak
mv {file}.bak {file}
```

### Option C: Reset to Last Commit
```bash
git reset --hard HEAD
```
⚠️ **Destroys all changes since last commit**

### Option D: Reset to Specific Commit
```bash
git log --oneline -10
git reset --hard {commit-hash}
```
⚠️ **Destroys all changes since that commit**

### Option E: Create Recovery Branch
```bash
git stash
git checkout -b recovery/{date}
git stash pop
```
Saves current mess for later analysis.

---

## Step 4: Verify Recovery

```bash
git status
pytest tests/unit/ -v --tb=short
```

---

## Step 5: Document What Happened

Add to `docs/working/incident_{date}.md`:
```markdown
# Incident {date}

## What went wrong
{description}

## Recovery action taken
{Option used}

## Lessons learned
{What to avoid next time}
```

---

## Step 6: Fresh Start

```
🔄 ABORT COMPLETE

Recovery: {action taken}
Status: {clean/needs work}

Recommend: Start fresh chat with `/start-session`
```

---

## Quick Commands Reference

| Situation | Command |
|-----------|---------|
| Undo file changes | `git checkout -- {file}` |
| Undo all changes | `git checkout -- .` |
| Remove untracked files | `git clean -fd` |
| Hard reset | `git reset --hard HEAD` |
| See recent commits | `git log --oneline -10` |
| Stash for later | `git stash` |