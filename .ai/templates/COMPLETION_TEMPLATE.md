# {Component} Phase {N} Complete

**Date:** {Date}  
**Developer:** {Name}  
**Branch:** `{branch}`

---

## Summary

{Brief description of what was accomplished in this phase}

---

## Subagent Activity

### Implementer Results

| Action | Path | Lines | Status |
|--------|------|-------|--------|
| CREATE | `{path}` | {N} | ✅ |
| CREATE | `{path}` | {N} | ✅ |
| MODIFY | `{path}` | +{N} | ✅ |

**Total:** ~{X} lines created/modified

### Tester Results

| Path | Tests | Status |
|------|-------|--------|
| `{test_path}` | {N} | ✅ |
| `{test_path}` | {N} | ✅ |

**Total:** {X} tests passing

### Reviewer Results

| Severity | Count | Status |
|----------|-------|--------|
| CRITICAL | 0 | ✅ |
| HIGH | 0 | ✅ |
| MEDIUM | {N} | {Tracked/Fixed} |
| LOW | {N} | {Optional} |

**Verdict:** {APPROVED / APPROVED WITH NOTES}

---

## Test Results

- **Tests:** {X} passing
- **Coverage:** {Y}% (if measured)
- **Command:** `pytest tests/unit/{component}/ -v`

---

## Key Decisions

1. **{Decision 1}:** {Brief explanation}
2. **{Decision 2}:** {Brief explanation}

---

## Changes from Plan

{List any deviations from the handoff plan, or "None - implemented as planned"}

| Planned | Actual | Reason |
|---------|--------|--------|
| {what was planned} | {what was done} | {why} |

---

## Task Constants Updates

**Added this phase:**

| Item | Value | Notes |
|------|-------|-------|
| {new item} | `{value}` | {why added} |

**Preserved from previous:**

| Item | Value | Established |
|------|-------|-------------|
| {existing} | `{value}` | Phase {N} |

---

## Learnings

{Any insights or things to remember for future phases/projects}

- {Learning 1}
- {Learning 2}

---

## 🔒 Task Constants Archive (Final Phase Only)

<!-- Include this section ONLY if this is the FINAL phase of the task -->

These were the key invariants throughout this task:

| Item | Value | Established | Used By |
|------|-------|-------------|---------|
| {item} | `{value}` | Phase {N} | {which phases} |

These can now be modified freely as the task is complete.

---

## Next Steps

### If NOT Final Phase:

- [ ] Commit: `git add . && git commit -m "Phase {N} complete: {summary}"`
- [ ] Create handoff: `docs/tasks/{component}_phase{N+1}_handoff.md`
- [ ] Update `dev_context.md` with Phase {N+1} info
- [ ] Continue to Phase {N+1}: {Phase Name}

**Next Phase Preview:**
- Goal: {next phase goal}
- Implementer: {what they'll create}
- See: `docs/tasks/{component}_phase{N+1}_handoff.md`

### If Final Phase:

- [ ] Task complete! 🎉
- [ ] Commit: `git add . && git commit -m "Feature complete: {feature}"`
- [ ] Branch ready for merge/PR
- [ ] Remove Task Constants from `dev_context.md`
- [ ] Archive this doc to `docs/tasks/completed/`

---

*Completed: {Date Time}*