# Phase [X] Start Prompt - [Feature Name]

**Use this prompt to start Phase [X] in a new Windsurf chat session.**

**Simply copy the entire prompt below (between the dashed lines) and paste it into a new chat.**

---

I'm [Ferran/Szabi]. Continue [Feature Name] Phase [X] implementation.

**Context to load:**
1. Read `dev[1/2]_context.md` (current status and session summary)
2. Read `docs/[FEATURE]_ARCHITECTURE.md` (comprehensive architecture)
3. Read `docs/[FEATURE]_PHASE[X]_HANDOFF.md` (Phase [X] handoff document)
4. Read `docs/tasks/[feature]_tasks.md` (overall task plan - optional)

**Current branch:** `feature/[branch-name]`  
**Current status:** Phase [X-1] COMPLETE ✅ ([X] tests passing)

**Phase [X-1] Completed:**
- ✅ [Component1] ([X] lines) - [Purpose]
- ✅ [Component2] ([X] lines) - [Purpose]
- ✅ [X] unit tests, all passing

**Next task: Phase [X] - [Phase Name]**

Create `src/[layer]/[component]`:
- [Specific requirement 1]
- [Specific requirement 2]
- [Specific requirement 3]
- Follow pattern from `src/[reference]/[file].py`
- Use [utility/library] for [purpose]

First, verify branch with: `git branch --show-current`

Then let's start by [specific first action to take].

---

## Quick Reference

**What's Done:**
- ✅ Phase 0: [Name] ([Deliverables])
- ✅ Phase [X-2]: [Name] ([Components])
- ✅ Phase [X-1]: [Name] ([Components])

**What's Next:**
- 📋 Phase [X]: [Name] ([Components to create])

**Key Files to Reference:**
- `[file path]` - [Pattern to follow]
- `[file path]` - [Recent example]
- `[file path]` - [Utility to use]

**Branch:** `feature/[branch-name]` ([X] commits, pushed to remote)

**Estimated Time:** [X]-[Y] hours

---

## Developer Notes

**Read these files before starting:**
- `docs/[FEATURE]_PHASE[X]_HANDOFF.md` - Complete implementation guide
- `src/[reference]/[file].py` - Pattern to follow
- `.github/copilot-instructions.md` - Coding standards (if unfamiliar)

**Success criteria for Phase [X]:**
- [Criterion 1]
- [Criterion 2]
- [X]+ tests passing
- All components < [X] lines

**After Phase [X] complete:**
- Commit with message: `feat([layer]): Phase [X] - [Name]`
- Push to remote
- Update `dev[1/2]_context.md`
- Create Phase [X+1] handoff and start prompt
