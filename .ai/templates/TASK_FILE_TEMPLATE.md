# Task: {Feature Name} Implementation

**Developer:** {Developer Name}
**Branch:** `feature/{feature-name}`
**Timeline:** {N} phases ({N} weeks)
**Priority:** {HIGH/MEDIUM/LOW} - Phase {N} of project
**Status:** {📋 Ready/🚧 In Progress/✅ Complete}

**Architecture Document:** `docs/{FEATURE}_ARCHITECTURE.md` (MUST READ FIRST)

---

## 📋 Overview

[2-3 sentence description of the feature and its purpose]

**Component Types:**
- **{Type1}** - {Purpose and responsibility}
- **{Type2}** - {Purpose and responsibility}
- **{Type3}** - {Purpose and responsibility}

---

## 🔒 Task Constants Tracking

**Purpose:** Track key decisions that must be preserved across ALL phases.

| Item | Value | Established | Status |
|------|-------|-------------|--------|
| *To be filled as phases progress* | | | |

**Rules:**
- Add items as key decisions are made in each phase
- Never remove items until task is FULLY complete
- Copy this section to each handoff doc AND dev context file

**What to track:**
- Test scripts with specific setup
- Constructor/method signatures that must not change
- Config structure keys
- Fixture file paths
- Key architectural decisions

---

## 🎯 Implementation Phases

### ✅ Phase 0: Architecture & Planning (COMPLETE)
**Goal:** [What this phase achieved]

**Deliverables:**
- ✅ [Deliverable 1]
- ✅ [Deliverable 2]

**Task Constants Established:** None yet

---

### 📋 Phase 1: {Phase Name} (Week 1 - Start Here)
**Goal:** {Specific, measurable goal for this phase}

**Components to Create:**
1. `src/{layer}/{component1}.py` - {Purpose and responsibilities}
2. `src/{layer}/{component2}.py` - {Purpose and responsibilities}

**Test Files:**
- `tests/unit/test_{component1}.py` - {What it tests}
- `tests/unit/test_{component2}.py` - {What it tests}

**Success Criteria:**
- {Specific, measurable criterion 1}
- {Specific, measurable criterion 2}
- {Test requirement - e.g., "10+ unit tests passing"}

**🔒 Expected Task Constants from Phase 1:**
- Integration test script (if created)
- Key constructor signatures
- Schema/model decisions

---

### 📋 Phase 2: {Phase Name} (Week 1)
**Goal:** {Specific, measurable goal for this phase}

**Components to Create:**
1. `src/{layer}/{component4}.py` - {Purpose}
2. `src/{layer}/{component5}.py` - {Purpose}

**Success Criteria:**
- {Specific criterion 1}
- {Specific criterion 2}

**🔒 Task Constants to Preserve:**
- All items from Phase 1
- Add new items as needed

---

### 📋 Phase 3: {Phase Name} (Week 2)
**Goal:** {Specific, measurable goal for this phase}

[Continue same structure...]

**🔒 Task Constants to Preserve:**
- All items from Phases 1-2

---

### 📋 Phase {N}: {Final Phase Name} (Week {N})
**Goal:** {Final integration/completion goal}

**🔒 Task Constants Handling:**
- Archive all constants to completion doc
- Remove constants section from dev context
- Constants can now be modified freely

---

## 🚀 Quick Start (For New Chat Session)

**First Prompt in New Chat:**
```
I'm {Name}. I'm starting {Feature} Phase {N} implementation.

Context to load:
1. Read dev_context.md or dev{N}_context.md (see .windsurf/team.md) - (current status + Task Constants)
2. Read docs/tasks/{feature}_phase{N}_handoff.md
3. Review 🔒 Task Constants before modifying any files

Current branch: feature/{feature-name}
Current task: Phase {N} - {Phase Name}

⚠️ Check Task Constants before creating/modifying test scripts or signatures.
```

---

## 📅 Phase Completion Tasks

**Every phase MUST include these final steps:**

```
- [ ] Run tests and validate implementation
- [ ] Update 🔒 Task Constants if new key items created
- [ ] Create Phase N completion doc + Phase N+1 handoff
- [ ] Copy Task Constants to handoff doc
```

**Final Phase ONLY:**
```
- [ ] Archive Task Constants to completion doc
- [ ] Remove Task Constants from dev context
- [ ] NO handoff doc needed (task complete)
```

---

## ✅ Success Criteria

**Minimum (Must Have):**
- {Core functionality requirement 1}
- {Core functionality requirement 2}
- All Task Constants preserved throughout

**Good (Should Have):**
- {Enhanced feature 1}
- {Enhanced feature 2}

---

## 🚨 Edge Cases to Handle

1. **{Edge case 1}** - {How to handle it}
2. **{Edge case 2}** - {How to handle it}

---

## 📊 Sample Input/Output

### Input: {Description}
```{language}
{Example input structure}
```

### Output: {Description}
```{language}
{Example output structure}
```

---

## 📁 Files to Create/Modify

```
src/{layer}/
├── {file1}.py                 # NEW - {Purpose}
├── {file2}.py                 # NEW - {Purpose}
└── {file3}.py                 # MODIFY - {What changes}

tests/
├── unit/
│   └── test_{component}.py    # NEW - {Test scope}
└── integration/
    └── test_{feature}.py      # NEW - Add to Task Constants!
```

---

## 📚 Key References

**Patterns to Follow:**
- `{existing file path}` - {What pattern to copy}

**Architecture Documents:**
- `docs/{FEATURE}_ARCHITECTURE.md` - Overall design
- `.ai/standards/{language}.md` - Coding standards

---

## ⚠️ Important Notes

### Task Constants Discipline
- **Add early:** When you create a test script or key signature, add it immediately
- **Never remove:** Until the entire task is complete
- **Sync always:** Constants must be identical in dev context AND handoff docs
- **Check first:** Before modifying any file, check if it's in Task Constants

### Code Quality Standards
- All files < 500-650 lines
- Type hints on all public methods
- Follow project coding standards

---

## 📅 Timeline & Estimates

**Total Estimated Time:** {N} weeks / {N} hours

**Phase Breakdown:**
- Phase 0: Architecture - {Hours}
- Phase 1: {Name} - {Hours} + establish initial Task Constants
- Phase 2: {Name} - {Hours}
- Phase {N}: {Name} - {Hours} + archive Task Constants

---

**Note:** This task uses Task Constants to preserve key decisions across phases. See `dev-context-template.md` for details.
