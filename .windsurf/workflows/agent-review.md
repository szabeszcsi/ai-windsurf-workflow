# Agent Review Workflow

Specific workflow for triggering the code review agent.

---

## Overview

The Reviewer agent performs structured code reviews focusing on quality, security, maintainability, and best practices. This workflow guides the review process from invocation to resolution.

---

## When to Use

| Scenario | Recommended |
|----------|-------------|
| Before committing significant changes | Yes |
| After implementing new feature | Yes |
| Before merging PR | Yes |
| Quick bug fix | Optional |
| Documentation changes only | No |
| Configuration changes | Yes (security focus) |

---

## Step 1: Prepare for Review

### Gather Scope Information

```markdown
## Review Request

**Files:** {list files or directories}
**Type:** New feature / Bug fix / Refactor / Security
**Focus Areas:** {specific concerns}
**Skip:** {what not to review}
```

### Check Prerequisites

- [ ] Code compiles/runs without errors
- [ ] Basic tests pass
- [ ] Files saved and staged
- [ ] Clear diff available

---

## Step 2: Invoke Reviewer

### Basic Invocation
```
/spawn-reviewer
```

### With Context
```
/spawn-reviewer

Files: src/auth/oauth.py, src/auth/tokens.py
Type: New feature
Focus: Security, error handling, edge cases
Skip: Existing utility functions
```

---

## Step 3: Review Process

The Reviewer agent will:

1. **Load role** from `.ai/agents/reviewer.md`
2. **Read target files** specified in scope
3. **Check against standards** in `.ai/standards/`
4. **Apply review checklist** (see below)
5. **Produce structured findings**

### Review Checklist Applied

- [ ] Logic correctness
- [ ] Error handling
- [ ] Edge cases
- [ ] Security vulnerabilities
- [ ] Performance concerns
- [ ] Code style compliance
- [ ] Documentation adequacy
- [ ] Test coverage indicators

---

## Step 4: Review Output

### Expected Format

```markdown
## Reviewer Analysis

**Scope:** src/auth/ - OAuth implementation
**Files:** oauth.py, tokens.py (243 lines total)
**Standards Applied:** python.md

### Findings

**Critical (Must Fix):**
1. [oauth.py:45] SQL injection vulnerability in user lookup
2. [tokens.py:78] Token expiry not validated

**Important (Should Fix):**
3. [oauth.py:112] Exception too broad, catches all errors
4. [tokens.py:23] Missing type hints on public function

**Minor (Consider):**
5. [oauth.py:67] Magic number 3600, use named constant
6. [tokens.py:91] Redundant else after return

### Recommendations
1. Use parameterized queries for all database operations
2. Add token expiry check before accepting refresh
3. Narrow exception handling to specific error types

### Out of Scope
- Did NOT review: test files, migrations, existing utils
- Did NOT check: integration tests, deployment config

### Handoff
**To Implementer:** Fix critical items 1-2 before merge
**Priority:** HIGH
```

---

## Step 5: Process Findings

### Triage Findings

| Severity | Action | Timeline |
|----------|--------|----------|
| Critical | Must fix | Before commit |
| Important | Should fix | This PR or next |
| Minor | Consider | Backlog |

### Create Action Items

For each accepted finding:
```markdown
- [ ] Fix [file:line] - {description}
```

---

## Step 6: Resolution Options

### Fix Now
1. Address findings
2. Re-run review on changed files only
3. Verify fixes pass

### Defer with Justification
```markdown
**Deferred:** Finding #5 (magic number)
**Reason:** Will address in configuration refactor phase
**Tracking:** Added to backlog as TECH-123
```

### Reject with Explanation
```markdown
**Rejected:** Finding #6 (redundant else)
**Reason:** Improves readability in this context per team standard
```

---

## Step 7: Review Complete

### Update dev_context.md

```markdown
## Recent Reviews

| Date | Scope | Findings | Status |
|------|-------|----------|--------|
| 2024-02-11 | src/auth/ | 2 critical, 2 important | Fixed |
```

### Clear Agent Status

```markdown
## Active Agents

| Agent | Status | Task | Started |
|-------|--------|------|---------|
| - | - | - | - |
```

---

## Review-Implement Loop

When fixes needed:

```
┌─────────────┐
│   Review    │
└──────┬──────┘
       │ Findings
       ▼
┌─────────────┐
│ Implement   │
│   Fixes     │
└──────┬──────┘
       │ Changes
       ▼
┌─────────────┐
│  Re-Review  │◄──────┐
│ (Changed)   │       │
└──────┬──────┘       │
       │ New Issues?  │
       ▼              │
   ┌───────┐    Yes   │
   │Issues?│──────────┘
   └───┬───┘
       │ No
       ▼
┌─────────────┐
│   Approve   │
└─────────────┘
```

See: `.ai/coordination/review-workflow.md` for detailed handoff patterns.

---

## Quick Reference

| Step | Action | Output |
|------|--------|--------|
| 1 | Prepare scope | Review request |
| 2 | `/spawn-reviewer` | Agent activated |
| 3 | Agent reviews | Structured findings |
| 4 | Triage findings | Action items |
| 5 | Fix or defer | Resolution decisions |
| 6 | Verify | Review complete |

---

## Related Files

- Reviewer agent: `.ai/agents/reviewer.md`
- Review workflow: `.ai/coordination/review-workflow.md`
- Coding standards: `.ai/standards/`
- Spawn workflow: `.ai/workflows/spawn-agent.md`
