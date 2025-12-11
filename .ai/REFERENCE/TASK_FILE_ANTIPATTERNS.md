# Task File Anti-Patterns

**Purpose:** Common mistakes to avoid when creating phase-based task files.

---

## ❌ Anti-Pattern 1: Vague Phase Goals

### Bad Example
```markdown
### Phase 1: Setup
**Goal:** Setup the project

- Setup some files
- Do initial work
- Get things ready
```

**Why it's bad:**
- No specific deliverables
- Can't measure completion
- No clear success criteria
- Impossible to test

### Good Example
```markdown
### Phase 1: Core Parsing (Week 1)
**Goal:** Parse PBIR files and extract page/visual structure with data bindings

**Components to Create:**
1. src/ui_layer/parsers/pbir_parser.py - Main PBIR orchestrator
2. src/ui_layer/parsers/page_parser.py - Extract page definitions
3. src/ui_layer/parsers/visual_parser.py - Extract visual definitions

**Success Criteria:**
- Parse complete PBIR folder structure (100% of files)
- Extract all pages and visuals with positions
- Extract data bindings (measures/columns)
- 13+ unit tests passing
- Parse sample report in < 2 seconds

**Test Files:**
- tests/unit/test_pbir_parser.py (5+ tests)
- tests/unit/test_page_parser.py (4+ tests)
- tests/unit/test_visual_parser.py (6+ tests)
```

**Why it's good:**
- Specific components to create
- Measurable success criteria
- Clear test requirements
- Performance target included

---

## ❌ Anti-Pattern 2: Phases Too Large

### Bad Example
```markdown
### Phase 1: Complete Implementation (Week 1-3)
**Goal:** Build entire system

**Tasks:**
- Build all parsers
- Add all analyzers
- Create all enrichers
- Generate all outputs
- Write all tests
- Deploy to production
```

**Why it's bad:**
- 3 weeks in single chat = massive context issues
- Too many moving parts
- Can't test incrementally
- Impossible to maintain focus

### Good Example
Break into smaller, focused phases:

```markdown
### Phase 1: Core Parsing (2-4 hours)
**Goal:** Parse PBIR files and extract structure
**Deliverables:** 3 parsers, 13 tests

### Phase 2: Data Binding Analysis (2-4 hours)
**Goal:** Analyze measure and column usage
**Deliverables:** 2 analyzers, 28 tests

### Phase 3: AI Enrichment (3-4 hours)
**Goal:** Add AI-generated narratives
**Deliverables:** 2 enrichers, 21 tests

### Phase 4: Output Generation (2-3 hours)
**Goal:** Generate JSON/Excel/Markdown
**Deliverables:** 1 generator, 27 tests

### Phase 5: Integration (2-3 hours)
**Goal:** Orchestrate full pipeline
**Deliverables:** 1 orchestrator, 16 tests
```

**Why it's good:**
- Each phase = 1 chat session
- Clear boundaries and goals
- Incremental testing
- Fresh context for each phase

---

## ❌ Anti-Pattern 3: Missing Test Requirements

### Bad Example
```markdown
### Phase 1: Create parser
**Goal:** Parse files

**Success Criteria:**
- Parser works
- Can read files
```

**Why it's bad:**
- No test files specified
- No coverage requirements
- Can't verify "works"
- No way to prevent regression

### Good Example
```markdown
### Phase 1: Core Parsing
**Goal:** Parse PBIR files and extract structure

**Test Files:**
- tests/unit/test_pbir_parser.py (5+ tests)
- tests/unit/test_page_parser.py (4+ tests)
- tests/unit/test_visual_parser.py (6+ tests)

**Success Criteria:**
- All 13+ unit tests passing
- 80%+ code coverage on new code
- Parse tests/fixtures/sample_reports/minimal_report/ without errors
- Parse tests/fixtures/sample_reports/complex_report/ in < 5 seconds
- Handle corrupted files gracefully (error tests)

**Test Cases Required:**
- Happy path: Parse valid PBIR
- Edge case: Empty report (0 visuals)
- Edge case: Large report (100+ visuals)
- Error: Missing Report.json
- Error: Corrupted JSON
- Error: Permission denied
```

**Why it's good:**
- Specific test file names
- Minimum test count
- Coverage requirement
- Happy path + edge cases + errors
- Performance criteria
- Can't commit until tests pass

---

## ❌ Anti-Pattern 4: No Ready-to-Use Prompts

### Bad Example
```markdown
### Task 1.1: Create the parser
- Create PBIRParser class
- Add methods to parse files
- Make it work
- Test it
```

**Why it's bad:**
- Too vague for AI assistant
- No specific guidance
- No pattern to follow
- No success criteria

### Good Example
```markdown
### Task 1.1: Create PBIRParser (2 hours)
**Goal:** Main parser that orchestrates page and visual parsing

**Windsurf Prompt:**
```
Create the main PBIR parser class.

File: src/ui_layer/parsers/pbir_parser.py

Based on docs/UI_LAYER_ARCHITECTURE.md design:
1. Create PBIRParser class that parses PBIR folder structure
2. Implement parse_report() method returning ReportStructure
3. Coordinate PageParser and VisualParser
4. Add comprehensive error handling for:
   - Missing Report.json
   - Corrupted JSON files
   - Permission errors
5. Add logging using common.logger
6. Add type hints and docstrings

Pattern to follow: src/model_layer/extractors/xmla_extractor.py
- Use same initialization pattern
- Same error handling approach
- Same logging format

Class structure:
```python
class PBIRParser:
    """Parse PBIR folder and extract report structure."""
    
    def __init__(self, report_path: Path, logger: Logger):
        """Initialize with path validation."""
        
    def parse_report(self) -> ReportStructure:
        """Main entry point - parses complete report."""
        
    def _validate_pbir_structure(self) -> bool:
        """Verify PBIR folder structure is valid."""
        
    def _parse_report_json(self) -> Dict:
        """Parse Report.json file."""
```

Success criteria:
- Parse tests/fixtures/sample_reports/minimal_report/ successfully
- All errors return clear error messages
- Logging shows progress for each step
- Returns ReportStructure with pages and visuals
```
```

**Why it's good:**
- Ready to copy-paste into Windsurf
- Specific file and location
- Reference to pattern
- Code structure provided
- Clear success criteria
- Developer can start immediately

---

## ❌ Anti-Pattern 5: Missing Context for New Chats

### Bad Example
```markdown
### Phase 2: Continue work

Start Phase 2.
```

**Why it's bad:**
- No context files listed
- Don't know which branch
- Don't know what was completed
- New chat starts blind

### Good Example
```markdown
## 🚀 Quick Start (For New Chat Session)

**First Prompt in New Chat:**
```
I'm Szabi. I'm starting UI Layer Phase 2 implementation.

Context to load:
1. Read dev2_context.md (current status and recent completions)
2. Read docs/UI_LAYER_ARCHITECTURE.md (comprehensive architecture)
3. Read docs/UI_LAYER_PHASE2_HANDOFF.md (Phase 2 specific guide)
4. Read docs/tasks/ui_parser_tasks.md (this file - optional)

Current branch: feature/ui-layer-pbir
Current status: Phase 1 COMPLETE ✅ (13 tests passing)

Phase 1 completed:
- ✅ PBIRParser (456 lines)
- ✅ PageParser (217 lines)
- ✅ VisualParser (387 lines)
- ✅ 13 unit tests, all passing

Next task: Phase 2 - Data Binding Analysis
- Create src/ui_layer/analyzers/measure_usage_analyzer.py
- Create src/ui_layer/analyzers/data_binding_analyzer.py
- Follow pattern from Model Layer analyzers
- Cross-reference with Model Layer metadata

First, verify branch with: git branch --show-current

Then let's start by creating the analyzers folder structure and MeasureUsageAnalyzer class.
```

**Quick Reference:**
- Branch: feature/ui-layer-pbir
- Previous: Phase 1 (Parsing) - 13 tests ✅
- Current: Phase 2 (Analysis) - 28 tests target
- Files to reference:
  - src/model_layer/extractors/measure_extractor.py (pattern)
  - src/ui_layer/parsers/pbir_parser.py (data source)
```

**Why it's good:**
- Complete ready-to-paste prompt
- Lists all context files to load
- Shows current branch
- Summarizes previous phase
- Clear next actions
- Reference files listed
- AI can start immediately with full context

---

## ❌ Anti-Pattern 6: No Handoff Documentation

### Bad Example
End of phase:
```bash
git add .
git commit -m "done"
git push
```

Move to next chat and start fresh with no guidance.

**Why it's bad:**
- Next chat has no context
- No guide for next phase
- Don't know what was completed
- Have to re-discover decisions

### Good Example
At end of Phase 1, create 3 documents:

**1. Update dev context** (dev2_context.md):
```markdown
## Current Work
✅ Completed: Phase 1 - Core Parsing
  - PBIRParser (456 lines, 5 tests)
  - PageParser (217 lines, 4 tests)
  - VisualParser (387 lines, 6 tests)
🔧 Next: Phase 2 - Data Binding Analysis
📍 Branch: feature/ui-layer-pbir - 1 commit, pushed
```

**2. Create Phase 2 handoff** (docs/UI_LAYER_PHASE2_HANDOFF.md):
- Complete implementation guide (300+ lines)
- Current status summary
- Phase 2 goals and components
- Implementation steps with code examples
- References to patterns
- Success criteria

**3. Create Phase 2 start prompt** (PHASE2_START_PROMPT.md):
- Ready-to-paste prompt for new chat
- Context files to load
- Current branch and status
- Next actions

**4. Provide end-of-phase prompt:**
```markdown
Phase 1 complete! 🎉

**What was delivered:**
- ✅ PBIRParser (456 lines, 5 tests)
- ✅ PageParser (217 lines, 4 tests)
- ✅ VisualParser (387 lines, 6 tests)
- ✅ All 13 tests passing
- ✅ Branch committed and pushed

**Documentation created for next session:**
- `PHASE2_START_PROMPT.md` - Copy this into new chat
- `docs/UI_LAYER_PHASE2_HANDOFF.md` - Implementation guide
- `dev2_context.md` - Updated with completion

**To start Phase 2 in a new chat:**
Simply copy the contents of `PHASE2_START_PROMPT.md` into a new chat session.

**Branch status:** All changes committed to `feature/ui-layer-pbir`

Ready for Phase 2! 🚀
```

**Why it's good:**
- Complete handoff documentation
- Next chat has full guidance
- Decisions and learnings captured
- Developer can resume immediately
- No context loss between chats

---

## ❌ Anti-Pattern 7: No Code Examples in Prompts

### Bad Example
```markdown
Create a parser that reads files and extracts data.
Follow best practices.
```

**Why it's bad:**
- AI has to guess structure
- May not match project patterns
- Wastes time on iterations

### Good Example
```markdown
**Windsurf Prompt:**
```
Create MeasureUsageAnalyzer.

File: src/ui_layer/analyzers/measure_usage_analyzer.py

Pattern: Follow src/model_layer/extractors/measure_extractor.py

Implementation:
```python
class MeasureUsageAnalyzer:
    """Analyze measure usage across report visuals."""
    
    def __init__(self, report_data: Dict, model_metadata: Optional[Dict], logger: Logger):
        """
        Initialize analyzer.
        
        Args:
            report_data: Parsed report structure from PBIRParser
            model_metadata: Optional Model Layer metadata for cross-reference
            logger: Logger instance
        """
        self.report_data = report_data
        self.model_metadata = model_metadata
        self.logger = logger
        
    def analyze(self) -> Dict[str, Any]:
        """
        Analyze measure usage across all visuals.
        
        Returns:
            Dict containing:
            - measure_usage: Dict[measure_name, List[visual_names]]
            - unused_measures: List[measure_names]
            - orphaned_visuals: List[visuals with unknown measures]
        """
        self.logger.info("Starting measure usage analysis")
        
        measure_usage = self._extract_measure_usage()
        unused = self._find_unused_measures(measure_usage)
        orphaned = self._find_orphaned_visuals(measure_usage)
        
        return {
            "measure_usage": measure_usage,
            "unused_measures": unused,
            "orphaned_visuals": orphaned
        }
```

Use:
- common.logger for logging
- Type hints on all methods
- Google-style docstrings
- Try/except with specific exceptions

Test with: tests/fixtures/sample_reports/minimal_report/
```
```

**Why it's good:**
- Shows exact structure expected
- Includes docstrings
- Shows method signatures
- References project utilities
- AI can implement immediately

---

## ❌ Anti-Pattern 8: Ignoring Project Rules

### Bad Example
Create task file without reading:
- copilot-instructions.md
- windsurfrules.md
- PROJECT_STATUS.md

Result: Task file doesn't follow project patterns.

### Good Example
Before creating task file:

**1. Read project rules:**
```markdown
Read these files first:
1. PROJECT_STATUS.md - Current state
2. .github/copilot-instructions.md - Universal standards
3. .windsurf/rules/windsurfrules.md - Windsurf patterns
4. Similar task files - docs/tasks/*.md
```

**2. Incorporate rules:**
```markdown
Task file must include:
- Developer identification (Ferran/Szabi)
- Context file loading instructions
- File size limits (< 500-650 lines)
- Test requirements (80%+ coverage)
- Commit only when tests pass
- Update dev context after each phase
- Archive when context > 1.5KB
- Follow coding standards
```

**3. Verify compliance:**
```markdown
Checklist:
- [ ] Respects file size limits
- [ ] Specifies test requirements
- [ ] Includes context management
- [ ] References coding standards
- [ ] Has handoff process
- [ ] Has start prompts
```

**Why it's good:**
- Task file fits project workflow
- Follows established patterns
- Respects project constraints
- Enables smooth multi-chat development

---

## ✅ Summary: Key Principles

### DO:
- ✅ Create specific, measurable phase goals
- ✅ Keep phases small (2-4 hours each)
- ✅ Include comprehensive test requirements
- ✅ Provide ready-to-paste Windsurf prompts
- ✅ Create handoff documentation for each phase
- ✅ Include code structure examples
- ✅ Specify context files for new chats
- ✅ Follow project rules and patterns

### DON'T:
- ❌ Make vague goals like "setup" or "fix things"
- ❌ Create large phases (3+ weeks)
- ❌ Skip test requirements
- ❌ Provide vague task descriptions
- ❌ Forget to document handoffs
- ❌ Leave AI guessing about structure
- ❌ Start new chats without context
- ❌ Ignore project-specific rules

---

**Remember:** The goal is productive multi-chat development with zero context degradation!
