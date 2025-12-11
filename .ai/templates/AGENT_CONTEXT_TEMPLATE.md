# Agent Context: {Agent Type}

**Agent ID:** {unique-id}
**Type:** Reviewer | Architect | Tester | Implementer | Coordinator
**Session:** {start timestamp}
**Status:** Active | Paused | Blocked | Complete

---

## Assignment

**Task:** {task description}
**Priority:** HIGH | MEDIUM | LOW
**Deadline:** {if any}
**Assigned by:** {coordinator/user}

---

## Scope

### Exclusive Files (I can modify)
```
{path/pattern}
{path/pattern}
```

### Read-Only (Reference only)
```
{path/pattern}
```

### Off-Limits (Do not touch)
```
{path/pattern}
```

---

## Context Received

### From Handoff
**Source:** {agent/user}
**Key Points:**
- {point 1}
- {point 2}

### Task Constants
| Item | Value | Notes |
|------|-------|-------|
| {constant} | {value} | DO NOT CHANGE |

### References
- Architecture: `SOLUTION_ARCHITECTURE.md`
- Standards: `.ai/standards/{language}.md`
- Related: `{other files}`

---

## Progress

### Completed
- [ ] {step 1}
- [ ] {step 2}

### In Progress
- {current work}

### Pending
- {remaining work}

### Blockers
- {if any}

---

## Decisions Made

| Decision | Rationale | Impact |
|----------|-----------|--------|
| {what} | {why} | {files affected} |

---

## Files Modified

| File | Action | Status |
|------|--------|--------|
| `{path}` | Created/Modified | Done/WIP |

---

## Questions/Clarifications Needed

- [ ] {question 1}
- [ ] {question 2}

---

## Coordination

### Parallel Agents
| Agent | Task | Interaction |
|-------|------|-------------|
| {id} | {task} | None / Waiting / Sharing |

### Dependencies
- **I need from:** {agent} - {what}
- **Others need from me:** {agent} - {what}

---

## Session Health

**Context Usage:** {if known}%
**Symptoms:** None | Re-reading files | Confusion | Other
**Recommendation:** Continue | Save progress | New session

---

## Handoff Preparation

When complete, provide:

```markdown
## Handoff: {this agent} → {next agent}

**Work Completed:**
{summary}

**Files Created/Modified:**
{list}

**Key Decisions:**
{what was decided and why}

**Remaining Work:**
{what's left}

**Recommendations:**
{advice for next agent}
```

---

## Exit Checklist

Before completing session:

- [ ] All scope files committed/saved
- [ ] Progress documented
- [ ] Handoff prepared (if needed)
- [ ] team_context.md updated
- [ ] No orphaned work

---

*Template version: 1.0*
*See: `.ai/agents/_agent-protocol.md`*
