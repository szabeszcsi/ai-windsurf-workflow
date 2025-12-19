---
name: phase-complete
description: Phase completion protocol. Run when all phase tasks and tests pass.
auto_execution_mode: 0
---

# Phase Complete

## Pre-Flight

- [ ] All phase tasks done
- [ ] All tests passing
- [ ] On correct branch

**If any unchecked:** Complete first.

---

## 1. Run Tests

```bash
pytest tests/unit/ -v
pytest tests/integration/ -v
```

**⚠️ If any tests fail, ABORT this workflow and fix the tests first.**

Do not proceed with phase completion until ALL tests pass.

---

## 2. Update Tech Summaries

For each module created/modified:
```
/generate-tech-summary
Layer: {layer}
Module: {module}
```

---

## 3. Create Docs

**Completion doc:** `docs/tasks/{component}_phase{N}_complete.md`
```markdown
# {Component} Phase {N} Complete

**Date:** {date}
**Developer:** {name}
**Branch:** {branch}

## Summary
{What was accomplished}

## Deliverables
| File | Lines | Purpose |
|------|-------|---------|
| {path} | {N} | {desc} |

## Tests
{X} tests passing
```

**Next handoff (if not final):** `docs/tasks/{component}_phase{N+1}_handoff.md`
- Copy 🔒 Task Constants
- Define phase goals and steps

---

## 4. Update Context

In `dev_context.md`:
- Add to ✅ Recent Completions
- Update 🎯 Primary Task to Phase {N+1}

Archive old handoff:
```bash
mv docs/tasks/{component}_phase{N}_handoff.md docs/tasks/completed/
```

---

## 5. Git Commit

```bash
git add .
git commit -m "feat({component}): Complete Phase {N}"
git push origin {branch}
```

---

## 6. Report

```
🎉 PHASE {N} COMPLETE

✅ Tests passed
✅ Completion doc created
✅ Tech summaries updated
✅ Handoff created (if applicable)
✅ Context updated
✅ Committed and pushed

⚠️ START PHASE {N+1} IN NEW CHAT

Copy to start:
---
/start-session
Task: {Component} Phase {N+1}
---
```

---

## Final Phase

If last phase:
- No handoff needed
- Archive Task Constants to completion doc
- Remove 🔒 section from dev_context
