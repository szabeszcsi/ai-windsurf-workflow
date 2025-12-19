---
trigger: model
description: Enforce phase-complete discipline when user claims done (model-decision fallback)
---

# Phase Complete Guard

**Apply when user indicates:**
- "phase complete"
- "done"
- "tests pass"
- "ready to merge"
- "PR ready"

---

## Required Response

Direct session into `/phase-complete` workflow.

**Do not accept completion without:**
- [ ] Tests run (unit + integration if applicable)
- [ ] Tech summaries updated for modified modules
- [ ] Completion doc written
- [ ] Dev context updated

---

## Exit Criteria

Only report completion after all required artifacts done.

Then instruct: **Start next phase in NEW CHAT → `/start-session`**
