# AI Task File Generation Guide

**Purpose:** Teach AI tools how to create effective phase-based task files that enable multi-chat development with optimal context management.

**Last Updated:** November 30, 2025  
**Success Pattern:** UI Layer implementation (5 phases, 5 chats, 105 tests, 6,335 lines)

---

## 🎯 Why Phase-Based Task Files?

### The Problem
Long development tasks in single chat sessions lead to:
- **Context degradation** - AI "forgets" earlier decisions
- **Token overflow** - Conversation becomes unwieldy
- **Lost progress** - Hard to pick up where you left off
- **Poor handoffs** - Next developer/session starts from scratch

### The Solution
Break work into **self-contained phases**, each completing in a separate chat session:
- **Focused scope** - Each phase has clear goal and success criteria
- **Clean handoffs** - Every phase ends with documentation for next phase
- **Testable milestones** - Can't proceed until tests pass
- **Context efficiency** - New chat = fresh start with minimal context

### Real Results (UI Layer Example)
- **5 phases** across 5 separate chat sessions
- **Each phase:** 2-4 hours, self-contained, fully tested
- **Result:** 6,335 lines, 105 tests passing, zero context degradation
- **Developer feedback:** *"Very productive, keeping context optimal"*

---

## 📋 The Three-Document Pattern

Every phase requires three coordinated documents:

### 1. **Master Task File** (`docs/tasks/[feature]_tasks.md`)
- **Purpose:** Complete implementation guide for entire feature
- **Scope:** All phases, comprehensive reference
- **Updated:** As phases complete and requirements evolve
- **Audience:** AI and developer throughout entire feature

### 2. **Phase Handoff Document** (`docs/tasks/{layer}_phase{N}_handoff.md`)
- **Purpose:** Detailed implementation guide for ONE specific phase
- **Scope:** Single phase only
- **Created:** At END of current phase (before closing session)
- **Audience:** AI starting the specific phase

### 3. **Phase Start Prompt** (embedded in dev context file)
- **Purpose:** Ready-to-paste chat starter
- **Scope:** Single phase, minimal
- **Created:** At END of current phase (embedded in dev context)
- **Audience:** Developer starting new chat

---

## 🏗️ Document Templates

**See companion documents:**
- `TEMPLATES/TASK_FILE_TEMPLATE.md` - Master task file template
- `TEMPLATES/HANDOFF_DOC_TEMPLATE.md` - Phase handoff template
- `TEMPLATES/START_PROMPT_TEMPLATE.md` - Phase start prompt template

---

## 🎯 Critical Requirements for Each Phase

### 1. Goal Achievement ✅
Each phase MUST:
- Have a clear, measurable goal
- Deliver working, tested functionality
- Be self-contained (not dependent on uncommitted future work)
- Build incrementally on previous phases

**BAD:** "Improve the system"  
**GOOD:** "Parse PBIR files and extract page/visual structure with data bindings"



### 2. Testing Requirements ✅
Each phase MUST have:
- Unit tests for all new components (minimum 80% coverage)
- Tests that verify the phase goal is achieved
- All tests passing before commit

**Test naming:**
- Unit: `tests/unit/test_[component].py`
- Integration: `tests/integration/test_[layer]_[scope].py`

### 2.5. Phase Plan Structure (MANDATORY) ✅
When AI creates a task plan at the START of any phase, the plan MUST include these final steps:

```
- [ ] Run tests and validate implementation
- [ ] Create Phase N completion doc + Phase N+1 handoff   ← MANDATORY FINAL STEP
```

**Why this matters:**
- The handoff step is a **visible plan item** that must be explicitly completed
- Prevents AI from "finishing" when tests pass but before handoff docs are created
- Ensures continuity for the next session

**Phase Completion Checklist** (copy into plan):
```
- [ ] All tasks complete and tested
- [ ] Create `docs/tasks/{layer}_phase{N}_complete.md`
- [ ] Create `docs/tasks/{layer}_phase{N+1}_handoff.md` (using HANDOFF_DOC_TEMPLATE.md)
```

The handoff step **cannot** be marked complete until BOTH documents exist.

**Workflow:** Use `/phase-complete` workflow to ensure all steps are completed.

### 3. Commit & Push Policy ✅
Phase can ONLY be committed/pushed when:
1. ✅ All phase components are complete
2. ✅ All tests are passing (`pytest`)
3. ✅ Code quality standards met (see below)
4. ✅ Documentation updated

**Code quality standards:**
- All files < 500-650 lines
- Type hints on public methods
- Docstrings on all classes/functions
- Follow project coding standards

**Commit message format:**
```
feat([layer]): Phase [X] - [Phase Name]

- [Component 1]
- [Component 2]
- [X] tests passing
```

### 4. Context & Documentation Maintenance ✅
At END of each phase, AI MUST:

**1. Update dev context file** (`dev1_context.md` or `dev2_context.md`):
```markdown
✅ Completed: Phase [X] - [Name]
  - [Component 1] ([X] lines, [Y] tests)
  - [Component 2] ([X] lines, [Y] tests)
🔧 Next: Phase [X+1] - [Name]
📍 Branch: feature/[branch] - [X] commits, pushed
```

**2. Create next phase handoff** (`docs/tasks/{layer}_phase{N+1}_handoff.md`):
- Comprehensive guide for next phase
- Include reference patterns and examples
- Implementation steps with code examples

**3. Embed start prompt in dev context file:**
- Ready-to-paste for new chat
- Lists exact context files to load
- Specifies first actions

**4. Follow project-specific rules:**
- Archive old sessions if context > 2KB
- Follow `.windsurf/rules/` patterns
- Follow `copilot-instructions.md` standards

### 5. Phase Completion Prompt ✅
At END of each phase, provide this in current chat:

```markdown
Phase [X] complete! 🎉

**What was delivered:**
- ✅ [Component 1] ([X] lines, [Y] tests)
- ✅ [Component 2] ([X] lines, [Y] tests)
- ✅ All tests passing ([Total] tests)
- ✅ Branch committed and pushed

**Documentation created for next session:**
- `docs/tasks/{layer}_phase{N+1}_handoff.md` - Implementation guide
- `dev[1/2]_context.md` - Updated with completion + start prompt

**To start Phase [X+1] in a new chat:**
Copy the start prompt from `dev[1/2]_context.md` into a new chat session.

**Branch status:** All changes committed to `feature/[branch]`

Ready for next phase! 🚀
```

### 6. Pull Request Creation (Final Phase Only) ✅
When ALL phases of a feature are complete, AI MUST propose PR creation:

**Prompt Template:**
```markdown
All phases complete! 🎉 Should I create a Pull Request to merge this to main?

**Branch:** feature/[name]
**Commits:** [X] commits, all pushed
**Tests:** [Y] tests passing
**Ready to merge:** Yes ✅

Create PR now? (Recommended: Yes)
```

**If Developer Says YES:**
1. Create PR using available tools (PyGithub or GitHub CLI)
2. Update dev context:
   ```markdown
   ⏳ PR #X: feature/[name] → main (created [date])
   - Status: Awaiting review/merge
   - Branch: Do not delete yet
   ```
3. Provide PR link to developer

**If Developer Says NO:**
Ask: "Merge locally instead or continue development?"

**Next Session Behavior:**
- AI checks pending PRs at session start
- Syncs with remote: `git pull origin main`
- Updates context if PR merged
- Asks about branch cleanup if merged

---

## 🔒 Task Constants Management

### What Are Task Constants?

Task Constants are **key decisions, files, and signatures** established during a task that must be preserved across ALL phases until the task is complete. They solve the problem of AI "helpfully" recreating or modifying working code in new chat sessions.

**Problem Solved:**
- Phase 2: Create `run_page_enrichment_test.py` with specific constructor
- Phase 3: New AI session doesn't know about the test
- Phase 3: AI tries to "fix" or recreate the test → 💥 Broken code

**Solution:**
```markdown
## 🔒 Task Constants (DO NOT MODIFY)
| Item | Value | Phase |
|------|-------|-------|
| Test script | `tests/integration/run_page_enrichment_test.py` | 1 |
| Constructor | `ReportDocumenter(config, ai_service, model_path)` | 1 |
```

### What Belongs in Task Constants

✅ **Include:**
- Integration test scripts with specific setup
- Constructor/method signatures that must not change
- Config structure keys (e.g., `ui_layer.selected_pages`)
- Fixture file paths
- Schema/model decisions (e.g., "V2 schema only")
- Key architectural choices
- "DO NOT" rules (e.g., "Don't re-enrich all 249 measures")

❌ **Exclude:**
- Session summaries (go in archive)
- Bug descriptions (go in Lingering)
- Progress updates (go in Primary Task section)
- Detailed code explanations (go in handoff docs)

### Task Constants Lifecycle

```
┌─────────────────────────────────────────────────────────────────┐
│ Phase 1                                                         │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ Create initial Task Constants as key decisions are made    │ │
│ │ → Test script created? Add it                              │ │
│ │ → Constructor signature decided? Add it                    │ │
│ └─────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ Phases 2 to N-1                                                 │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ Add new constants, NEVER remove existing ones              │ │
│ │ Copy constants to EVERY handoff doc                        │ │
│ │ AI checks constants BEFORE modifying any file              │ │
│ └─────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ Final Phase                                                     │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ Archive constants to completion doc                        │ │
│ │ Remove constants section from dev context                  │ │
│ │ Files can now be modified freely                           │ │
│ └─────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

### Size Limits

| Component | Limit |
|-----------|-------|
| Dev context (without constants) | < 1.5 KB |
| Task Constants section | < 500 bytes |
| **Total dev context** | < 2 KB |

**If Task Constants overflow (>500 bytes):**
1. Create `docs/working/{task}_constants.md` with full details
2. Keep summary in context file with reference:
   ```markdown
   ## 🔒 Task Constants
   **Details:** `docs/working/{task}_constants.md` ← LOAD THIS
   
   Summary:
   - Test: `tests/integration/...`
   - 8 key signatures (see details file)
   ```

### Where Task Constants Live

Constants must be **identical** in multiple locations (redundancy for safety):

1. **`dev{X}_context.md`** - Always loaded at session start
2. **`docs/tasks/{layer}_phase{N}_handoff.md`** - Loaded when starting phase
3. **Master task file** (optional) - For reference

### Integration with Workflows

**`/start-session`:**
```
✅ Session Ready
🔒 Task Constants loaded:
   - Test: tests/integration/run_page_enrichment_test.py
   - Constructor: ReportDocumenter(config, ai_service, model_path)
```

**`/update-context`:**
```
📝 SAVING PROGRESS

Did you create anything that future phases must NOT break?
[Y] Yes - add to Task Constants
[N] No - continue
```

**`/phase-complete`:**
- Non-final phase: Preserve constants, copy to handoff
- Final phase: Archive to completion doc, remove from context

### Example: UI Layer Refactoring Task

**Phase 1 - Constants Established:**
```markdown
## 🔒 Task Constants (DO NOT MODIFY)
**Task:** UI Layer Refactoring (Phases 1-5)

| Item | Value | Phase |
|------|-------|-------|
| Test script | `tests/integration/run_page_enrichment_test.py` | 1 |
| Constructor | `ReportDocumenter(config, ai_service, model_data_path)` | 1 |
| Schema | `src/ui_layer/models/output_schema.py` (V2) | 1 |
```

**Phase 4.5 - Constant Added:**
```markdown
| Enriched measures | Load from saved JSON, don't re-enrich | 4.5 |
```

**Phase 5 (Final) - Constants Archived:**
- Copied to `docs/tasks/ui_phase5_complete.md`
- Removed from `dev2_context.md`
- Files can now be modified

### Checklist for Task File Creation

When creating a new task file, include:

- [ ] `## 🔒 Task Constants Tracking` section in master task file
- [ ] "Expected Task Constants" note in Phase 1 section
- [ ] "Task Constants to Preserve" note in Phases 2+ sections
- [ ] "Archive Task Constants" step in final phase
- [ ] Task Constants section in HANDOFF_DOC_TEMPLATE
- [ ] Reference to `dev-context-template.md`

---

## 🤖 How AI Should Generate Task Files
!IMPORTANT: Always think it thru, take your time. Make a plan before doing any action.!

### Step 1: Gather Information
Ask the user:
1. "What feature are we implementing?"
2. "Which developer(s) will work on it?" (Ferran/Szabi/Both)
3. "What's the estimated timeline?" (weeks, complexity)
4. "What are the key requirements?" (user stories, acceptance criteria)
5. "Are there existing patterns to follow?" (reference other layers)
6. "What's the target architecture?" (OOP, functional, etc.)

### Step 2: Analyze Project Context
Read these files to understand project:
1. `PROJECT_STATUS.md` - Current state, layer status
2. `.github/copilot-instructions.md` - Universal coding standards
3. `.windsurf/rules/` - Windsurf rules (core-rules, coding-standards, windsurfrules)
4. Similar completed features - `docs/tasks/[reference]_tasks.md`
5. Architecture documents - `docs/[REFERENCE]_ARCHITECTURE.md`

### Step 3: Break Into Logical Phases
**Phase breakdown rules:**
- **Phase 0:** Architecture & Planning (if needed)
- **Each subsequent phase:** 2-4 hours of work
- **Each phase:** Delivers working, tested functionality
- **Phases build incrementally**

**Typical breakdown:**
1. **Phase 1:** Core components (parsing, extraction, etc.)
2. **Phase 2:** Analysis/processing
3. **Phase 3:** Enhancement (AI, enrichment)
4. **Phase 4:** Output generation
5. **Phase 5:** Integration/orchestration

**Example (UI Layer - 5 phases):**
- Phase 0: Architecture ✅
- Phase 1: Core Parsing (4 parsers, 13 tests)
- Phase 2: Data Binding Analysis (2 analyzers, 28 tests)
- Phase 3: AI Enrichment (2 enrichers, 21 tests)
- Phase 4: Output Generation (1 generator, 27 tests)
- Phase 5: Integration (1 orchestrator, 16 tests)

### Step 4: Define Success Criteria
For each phase, define:
1. **Specific deliverables** (files to create)
2. **Measurable outcomes** (X objects extracted, Y% accuracy)
3. **Test requirements** (minimum test count, coverage %)
4. **Performance targets** (if applicable)
5. **Integration points** (dependencies on other phases/layers)

**Success criteria format:**
```markdown
**Minimum (Must Have):**
- Core functionality working
- Basic tests passing

**Good (Should Have):**
- Enhanced features working
- Comprehensive tests

**Excellent (Nice to Have):**
- Optimizations implemented
- Edge cases handled
```

### Step 5: Create Detailed Task Prompts
For each task in each phase:
1. Write a ready-to-paste Windsurf prompt
2. Include context (what to read, patterns to follow)
3. Specify exact files to create
4. **Create actual files** - never paste implementation code in chat
5. Include code structure/pseudocode (brief, <10 lines)
6. Define success criteria

### Step 6: Generate All Three Documents
Generate in this order:

**First:** Main task file (`docs/tasks/{layer}_tasks.md`)
- Complete overview of all phases
- Comprehensive reference

**Then:** Phase 1 handoff (`docs/tasks/{layer}_phase1_handoff.md`)
- Detailed guide for first phase only
- Implementation steps and code examples

**Finally:** Phase 1 start prompt (embed in dev context file)
- Ready-to-paste prompt
- Context files to load

**For each subsequent phase:**
- Update main task file (mark previous complete)
- Create next phase handoff
- Create next phase start prompt

### Step 7: Integrate with Project Rules
Ensure task file respects:
1. Project coding standards (`copilot-instructions.md`)
2. File size limits (typically 500-650 lines max)
3. Testing requirements (unit + integration)
4. Documentation patterns (docstrings, type hints)
5. Context management (`.windsurf/rules/`)
6. Commit/push policies
7. Branch naming conventions

---

## ✅ Quality Checklist for Generated Task Files

### Structure ✅
- [ ] Clear overview with developer, branch, timeline, priority
- [ ] Phases are logically ordered and self-contained
- [ ] Each phase has specific goal and success criteria
- [ ] Quick start section for new chat sessions
- [ ] Sample input/output examples
- [ ] Files to create/modify section

### Content ✅
- [ ] Each task has ready-to-paste Windsurf prompt
- [ ] Code examples follow project patterns
- [ ] References to existing code for guidance
- [ ] Edge cases identified and handled
- [ ] Coordination points with other developers/layers noted
- [ ] Realistic time estimates provided

### Testing ✅
- [ ] Test requirements specified for each phase
- [ ] Test file naming follows conventions
- [ ] Both unit and integration tests planned
- [ ] Success criteria include "all tests passing"
- [ ] Test data/fixtures location specified

### Documentation ✅
- [ ] Links to architecture documents
- [ ] Links to reference implementations
- [ ] Links to coding standards
- [ ] Phase handoff documents planned
- [ ] Start prompts planned

### Context Management ✅
- [ ] Developer identification required
- [ ] Context files listed for each phase
- [ ] Dev context update triggers specified
- [ ] Archive policy mentioned
- [ ] Follow project-specific rules

### Commits & Quality ✅
- [ ] Commit only when all tests pass
- [ ] Code quality standards specified
- [ ] File size limits mentioned
- [ ] Branch strategy clear
- [ ] Handoff process documented

---

## 🚨 Common Anti-Patterns to Avoid

See `TASK_FILE_ANTIPATTERNS.md` for detailed examples of:
- ❌ Vague phase goals
- ❌ Phases too large
- ❌ Missing test requirements
- ❌ No ready-to-use prompts
- ❌ Missing context for new chats
- ❌ No handoff documentation
- ❌ **Task plan without handoff step as final item** - Always include "Create Phase N completion + handoff" in plan
- ❌ **Declaring phase complete before handoff exists** - Tests passing ≠ phase complete
- ❌ **Writing implementation code in chat** - Create files instead

---

## 📚 Real-World Example

### UI Layer Success Pattern

**Reference files:**
- `docs/tasks/ui_parser_tasks.md` - Master task file (478 lines)
- `docs/UI_LAYER_PHASE4_HANDOFF.md` - Example handoff doc (312 lines)
- `PHASE5_START_PROMPT.md` - Example start prompt (73 lines)

**Results:**
- 5 phases, 5 separate chat sessions
- 6,335 lines, 105 tests, zero context degradation
- Each phase: 2-4 hours, self-contained, fully tested
- Developer feedback: *"Very productive, keeping context optimal"*

**What Worked:**
1. **Clear Phase Boundaries** - Each phase had specific deliverables
2. **Comprehensive Documentation** - Handoff docs averaged 300 lines
3. **Ready-to-Paste Prompts** - Developer could start immediately
4. **Test-Driven Phases** - Couldn't proceed without tests passing
5. **Context Management** - New chat per phase = fresh context
6. **Consistent Patterns** - All components followed same OOP pattern

---

## 📖 Additional Resources

**Template Files (in TEMPLATES/):**
- `TEMPLATES/TASK_FILE_TEMPLATE.md` - Complete master task file template
- `TEMPLATES/HANDOFF_DOC_TEMPLATE.md` - Phase handoff document template
- `TEMPLATES/START_PROMPT_TEMPLATE.md` - Phase start prompt template

**Reference Files (in REFERENCE/):**
- `REFERENCE/TASK_FILE_ANTIPATTERNS.md` - Common mistakes to avoid
- `REFERENCE/TASK_FILE_EXAMPLES.md` - Annotated real-world examples
- `REFERENCE/FILE_ORGANIZATION_SUMMARY.md` - File placement guide

**Project Files:**
- `.github/copilot-instructions.md` - Coding standards
- `.windsurf/rules/` - Windsurf rules (core-rules, coding-standards, windsurfrules)
- `PROJECT_STATUS.md` - Current project state

---

## 🎓 Quick Start for AI Tools

When user asks you to create a task file:

1. **Ask questions** - Gather feature info, developer, timeline
2. **Read context** - PROJECT_STATUS.md, `.windsurf/rules/`
3. **Break into phases** - 2-4 hours each, testable milestones
4. **Use templates** - TASK_FILE_TEMPLATE.md, HANDOFF_DOC_TEMPLATE.md
5. **Generate all 3 docs** - Master task, Phase 1 handoff, Phase 1 start
6. **Verify quality** - Use checklist above
7. **Review with user** - Confirm phases make sense

**Remember:** The goal is to enable productive multi-chat development with optimal context management!

---
