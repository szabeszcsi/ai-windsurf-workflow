# {Component} Phase {N} Handoff

**Created:** {Date}  
**Developer:** {Name}  
**Branch:** `{branch}`  
**Status:** Phase {N-1} COMPLETE ✅ - Ready for Phase {N}

---

## 🔒 Task Constants (DO NOT MODIFY)

These were established in earlier phases and **MUST be preserved**.

| Item | Value | Established | Notes |
|------|-------|-------------|-------|
| Test script | `{path}` | Phase {X} | DO NOT RECREATE |
| Constructor | `{Class(params)}` | Phase {X} | DO NOT CHANGE |
| {Other} | `{value}` | Phase {X} | {notes} |

---

## Current Status

### Completed Phases

**Phase {N-1}: {Name}** ✅
- `{Component1}` ({X} lines) - {Purpose}
- `{Component2}` ({X} lines) - {Purpose}
- {X} tests passing

**Total Progress:**
- ~{X} lines of code
- {X} tests passing
- All components < 500 lines

---

## 🎯 Phase {N}: {Phase Name}

### Goal
{1-2 sentence clear description of what this phase achieves}

### Why This Matters
{Brief explanation of importance}

---

## Subagent Scopes

### Implementer Scope

| Action | Path | Purpose |
|--------|------|---------|
| CREATE | `src/{component}/{file1}.py` | {Purpose} |
| CREATE | `src/{component}/{file2}.py` | {Purpose} |
| MODIFY | `{existing_file}` | {What to change} |

**Off Limits:**
- `src/ui/` - Future phase
- `tests/` - Tester handles
- `{other paths}` - {reason}

**Constraints:**
- {Technical constraint 1}
- {Technical constraint 2}
- Follow `.ai/standards/{language}.md`

**Dependencies:**
- Uses: `{existing modules from previous phases}`
- New packages: `{any new requirements}`

---

### Tester Scope

| Action | Path | Target |
|--------|------|--------|
| CREATE | `tests/unit/{component}/test_{file1}.py` | {N}+ tests |
| CREATE | `tests/unit/{component}/test_{file2}.py` | {N}+ tests |

**Test Focus:**
- {What aspect 1 to test}
- {What aspect 2 to test}
- Error handling for {scenarios}

**Fixtures Needed:**
- `{fixture name}` - {purpose}

---

### Reviewer Scope

- **Files:** `{list of files Implementer creates}`
- **Focus:** {security / performance / error handling / general}
- **Standards:** `.ai/standards/{language}.md`
- **Special Attention:** {any specific concerns for this phase}

---

## Implementation Details

### {ComponentName} (~{X} lines)
**File:** `src/{component}/{file}.py`

**Responsibilities:**
- {Responsibility 1}
- {Responsibility 2}

**Pattern to Follow:**
Copy structure from `{reference_file}`

**Key Interface:**
```python
class {ComponentName}:
    """Brief description."""
    
    def __init__(self, {params}) -> None:
        """Initialize."""
        
    def {method1}(self, {params}) -> {ReturnType}:
        """Description."""
```

**Error Handling:**
- {How to handle error case 1}
- {How to handle error case 2}

---

## Implementation Steps

### Step 1: {Step Name}
**Goal:** {What this achieves}

**Implementer actions:**
1. {Specific action}
2. {Specific action}
3. {Specific action}

### Step 2: {Step Name}
**Goal:** {What this achieves}

**Implementer actions:**
1. {Specific action}
2. {Specific action}

### Step 3: Testing
**Goal:** Verify implementation

**Tester actions:**
1. Create test files per Tester Scope
2. Cover happy path, edge cases, errors
3. Run: `pytest tests/unit/{component}/ -v`

### Step 4: Review
**Goal:** Quality check

**Reviewer actions:**
1. Review files per Reviewer Scope
2. Check against standards
3. Report findings with severity

---

## References

- **Pattern:** `{file to follow}`
- **Architecture:** `SOLUTION_ARCHITECTURE.md`
- **Standards:** `.ai/standards/{language}.md`
- **Previous Phase:** `docs/tasks/{component}_phase{N-1}_complete.md`

---

## Success Criteria

Phase {N} is complete when:

| Criterion | Owner | Status |
|-----------|-------|--------|
| All Implementer files created | Implementer | ⏳ |
| Files follow standards | Implementer | ⏳ |
| {X}+ tests passing | Tester | ⏳ |
| No CRITICAL/HIGH issues | Reviewer | ⏳ |
| Task Constants preserved | All | ⏳ |
| All components < 500 lines | Implementer | ⏳ |

---

## After Phase {N}

**If more phases remain:**
- Create completion doc: `docs/tasks/{component}_phase{N}_complete.md`
- Create next handoff: `docs/tasks/{component}_phase{N+1}_handoff.md`
- Update `dev_context.md`

**Next Phase:** Phase {N+1} - {Name}
{1 sentence description}

**Update Task Constants if needed:**
- New test scripts → add
- New key signatures → add
- Never remove existing

---

## Start Prompt

Copy this to begin Phase {N}:

```
I'm {Name}. Starting {Component} Phase {N}.

Read:
1. dev_context.md
2. docs/tasks/{component}_phase{N}_handoff.md

Branch: {branch}

Phase {N} goal: {goal}
```

---

**Ready to start!** 🚀

First action: Verify Task Constants are in dev_context.md, then begin Implementer scope.