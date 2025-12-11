# Task: {Feature Name}

**Developer:** {Name}  
**Branch:** `feature/{feature-name}`  
**Timeline:** {N} phases ({estimate})  
**Priority:** {HIGH/MEDIUM/LOW}  
**Status:** {📋 Ready / 🚧 In Progress / ✅ Complete}

---

## Overview

{2-3 sentence description of the feature and its purpose}

---

## 🔒 Task Constants Tracking

Track key decisions that must be preserved across ALL phases.

| Item | Value | Established | Status |
|------|-------|-------------|--------|
| *Add as phases progress* | | | |

**Rules:**
- Add items as key decisions are made
- Never remove until task FULLY complete
- Copy to each handoff doc AND dev_context.md

---

## Phases

### ✅ Phase 0: Planning
**Goal:** Define architecture and implementation plan

**Deliverables:**
- ✅ SOLUTION_ARCHITECTURE.md updated
- ✅ This task file created
- ✅ Phase 1 handoff prepared

---

### 📋 Phase 1: {Phase Name}
**Goal:** {Specific, measurable goal}

#### Implementer Scope

| Action | Path | Purpose |
|--------|------|---------|
| CREATE | `src/{component}/{file1}.py` | {Purpose} |
| CREATE | `src/{component}/{file2}.py` | {Purpose} |
| MODIFY | `requirements.txt` | Add {packages} |

**Off Limits:** `src/ui/`, `tests/`, `config/`

**Constraints:**
- {Technical constraint 1}
- {Technical constraint 2}
- Follow `.ai/standards/{language}.md`

#### Tester Scope

| Action | Path | Target |
|--------|------|--------|
| CREATE | `tests/unit/{component}/test_{file1}.py` | {N}+ tests |
| CREATE | `tests/unit/{component}/test_{file2}.py` | {N}+ tests |

**Test Focus:** {What aspects to test - happy path, errors, edge cases}

#### Reviewer Scope

- **Files:** All files created by Implementer
- **Focus:** {security / performance / general}
- **Standards:** `.ai/standards/{language}.md`

#### Success Criteria

- [ ] All Implementer files created
- [ ] {N}+ tests passing
- [ ] Reviewer approval (no CRITICAL/HIGH issues)
- [ ] Task Constants updated if needed

---

### 📋 Phase 2: {Phase Name}
**Goal:** {Specific, measurable goal}

#### Implementer Scope

| Action | Path | Purpose |
|--------|------|---------|
| CREATE | `{path}` | {Purpose} |
| MODIFY | `{path}` | {What changes} |

**Off Limits:** {paths}

**Constraints:**
- {Constraints}

#### Tester Scope

| Action | Path | Target |
|--------|------|--------|
| CREATE | `{test path}` | {N}+ tests |

#### Success Criteria

- [ ] {Criterion 1}
- [ ] {Criterion 2}

---

### 📋 Phase N: {Final Phase}
**Goal:** {Final integration/completion goal}

#### Implementer Scope

| Action | Path | Purpose |
|--------|------|---------|
| MODIFY | `{main entry point}` | Integration |

#### Task Constants Handling

- Archive all constants to completion doc
- Remove from dev_context.md

#### Success Criteria

- [ ] All phases integrated
- [ ] Full test suite passing
- [ ] Ready for merge/PR

---

## Quick Start

**New chat prompt:**
```
I'm {Name}. Starting {Feature} Phase {X}.

Read:
1. dev_context.md
2. docs/tasks/{feature}_phase{X}_handoff.md

Branch: feature/{feature-name}
```

---

## Success Criteria (Overall)

**Minimum (Must Have):**
- {Core requirement 1}
- {Core requirement 2}

**Good (Should Have):**
- {Enhanced feature 1}

**Stretch:**
- {Nice to have}

---

## Files to Create (All Phases)

```
src/{component}/
├── {file1}.py              # Phase 1
├── {file2}.py              # Phase 1
└── {file3}.py              # Phase 2

tests/unit/{component}/
├── test_{file1}.py         # Phase 1
├── test_{file2}.py         # Phase 1
└── test_{file3}.py         # Phase 2
```

---

## References

- Architecture: `SOLUTION_ARCHITECTURE.md`
- Standards: `.ai/standards/{language}.md`
- Similar: `{reference to similar existing code}`
- Task Guide: `.ai/guides/TASK_FILE_GENERATION_GUIDE.md`

---

## Notes

{Any important context, constraints, or decisions}