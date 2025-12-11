# [Feature] Phase [X] Handoff - [Phase Name]

**Created:** [Date]  
**Developer:** [Ferran/Szabi]  
**Branch:** `feature/[branch-name]`  
**Status:** Phase [X-1] COMPLETE ✅ - Ready for Phase [X]

---

## 🔒 Task Constants (DO NOT MODIFY)

These items were established in earlier phases and **MUST be preserved**. Do not recreate, rename, or change signatures without explicit permission.

| Item | Path/Value | Established | Notes |
|------|------------|-------------|-------|
| Test script | `{path}` | Phase {N} | DO NOT RECREATE |
| Constructor | `{Class}({params})` | Phase {N} | DO NOT CHANGE SIGNATURE |
| Schema | `{path}` | Phase {N} | {version/notes} |
| Config key | `{key}` | Phase {N} | {notes} |
| Fixture | `{path}` | Phase {N} | DO NOT MODIFY |

<!-- Copy this section from dev{X}_context.md. Keep identical in both files. -->

---

## 📊 Current Status

### Completed (Phases [List Previous Phases])

**Phase [X-1]: [Name]** ✅
- `[Component1]` ([X] lines) - [Purpose]
- `[Component2]` ([X] lines) - [Purpose]
- `[Component3]` ([X] lines) - [Purpose]
- [X] unit tests, all passing ✅

**Phase [X-2]: [Name]** ✅
- `[Component4]` ([X] lines) - [Purpose]
- `[Component5]` ([X] lines) - [Purpose]
- [X] unit tests, all passing ✅

**Total Progress:**
- [X] commits on `feature/[branch]`
- ~[X] lines of production code
- [X] unit tests, all passing ✅
- All components < [X] lines
- Branch pushed to remote

---

## 🎯 Phase [X]: [Phase Name] (Next)

### Goal
[1-2 sentence clear, specific description of what this phase will achieve]

### Why This Phase Matters
[Brief explanation of why this phase is important and how it fits into the overall feature]

---

## 🏗️ Components to Create

### **[ComponentName1]** (~[X] lines)
**File:** `src/[layer]/[filename].py`

**Responsibilities:**
- [Responsibility 1 - what it does]
- [Responsibility 2 - what it handles]
- [Responsibility 3 - what it provides]

**Pattern to Follow:**
Copy structure from `src/[reference_layer]/[reference_file].py`
- [Pattern aspect 1 to copy]
- [Pattern aspect 2 to copy]
- [Pattern aspect 3 to adapt]

**Key Methods:**
```python
class [ComponentName]:
    """[Class purpose and responsibility]."""
    
    def __init__(self, [params]) -> None:
        """Initialize [component]."""
        
    def [method1](self, [params]) -> [ReturnType]:
        """[Method purpose and what it returns]."""
        
    def [method2](self, [params]) -> [ReturnType]:
        """[Method purpose and what it returns]."""
```

**Dependencies:**
- [External library or internal module]
- [Configuration or credential requirement]
- [Data from previous phase]

---

### **[ComponentName2]** (~[X] lines)
**File:** `src/[layer]/[filename].py`

[Same structure as ComponentName1]

---

## 📋 Implementation Steps

### Step 1: [Step Name]
**Goal:** [What this step achieves]

**Actions:**
1. [Specific action - what to create/modify]
2. [Specific action - what to implement]
3. [Specific action - what to test]

**Code Example:**
```python
[Example code structure or pseudocode showing the pattern]
```

---

### Step 2: [Step Name]
**Goal:** [What this step achieves]

**Actions:**
1. [Specific action]
2. [Specific action]
3. [Specific action]

---

## 🧪 Testing Strategy

### Unit Tests to Create

**`tests/unit/test_[component1].py`** ([X]+ tests):
- Test [method1] with valid input
- Test [method1] with edge cases
- Test [method2] with mock dependencies
- Test error handling for [scenario]

### Test Data

**Location:** `tests/fixtures/[feature]/[test_case]/`

### Testing Checklist
- [ ] All unit tests passing
- [ ] 80%+ code coverage
- [ ] Edge cases covered
- [ ] Error scenarios tested

---

## 🔗 Key References

### Reference Patterns (Study These First)
- `[file path]` - [What to learn: pattern, structure, approach]
- `[file path]` - [What to learn: error handling, logging, etc.]

### Architecture & Standards
- `docs/[FEATURE]_ARCHITECTURE.md` - Overall design
- `.github/copilot-instructions.md` - Coding standards

---

## ⚠️ Important Notes

### Common Pitfalls to Avoid
- ❌ [Anti-pattern 1]
- ❌ [Anti-pattern 2]
- ❌ **DO NOT modify Task Constants** without explicit permission

---

## 🚀 Success Criteria

**Phase [X] Complete When:**
- ✅ [Component1] created and tested
- ✅ [Component2] created and tested
- ✅ Unit tests passing ([X]+ tests)
- ✅ All components < [X] lines
- ✅ Task Constants preserved unchanged

**Expected Deliverables:**
- [X] [component type] (~[X] lines each)
- [X] test file (~[X] lines)

---

## 📅 Timeline

**Estimated Time:** [X]-[Y] hours

---

## 🔄 After Phase [X]

**Phase [X+1]: [Next Phase Name]**
[1-2 sentence description of what comes next]

**Update Task Constants if needed:**
- If you create new test scripts → add to constants
- If you establish key signatures → add to constants
- Never remove existing constants until task complete

---

**Ready to start Phase [X]!** 🚀

**First action:** Review Task Constants, then reference patterns.
