# Task File Real-World Examples

**Purpose:** Annotated examples from successful UI Layer implementation showing what works.

---

## 📚 Example 1: Master Task File Structure

**Source:** `docs/tasks/ui_parser_tasks.md` (478 lines)

### Opening Section - Clear Metadata
```markdown
# Task: UI Layer Implementation (PBIR Parsing)

**Developer:** Szabi  
**Branch:** `feature/ui-layer-pbir`  
**Timeline:** 5 phases (2-3 weeks)  
**Priority:** HIGH - Phase 3 of project  
**Status:** 📋 Architecture Complete - Ready for Implementation

**Architecture Document:** `docs/UI_LAYER_ARCHITECTURE.md` (MUST READ FIRST)
```

**Why this works:**
- ✅ Developer immediately identified (Szabi)
- ✅ Branch name clear and consistent
- ✅ Timeline realistic (5 phases over 2-3 weeks)
- ✅ Priority and project phase context
- ✅ Links to architecture document first

---

### Component Overview
```markdown
## 📋 Overview

Implement UI Layer to document Power BI reports by parsing PBIR files. 
Architecture follows Model Layer OOP pattern with 5 component types:
- **Parsers** - Extract from PBIR files
- **Enrichers** - AI enhancement
- **Analyzers** - Cross-layer linking
- **Generators** - Output creation
- **Utils** - Shared utilities
```

**Why this works:**
- ✅ Brief (2 sentences) but specific
- ✅ Shows component types clearly
- ✅ References existing pattern (Model Layer)
- ✅ Sets architectural expectations

---

### Phase Breakdown - Clear Goals
```markdown
### 📋 Phase 1: Core Parsing (Week 1 - Start Here)
**Goal:** Parse PBIR files and extract structure (no AI yet)

**Components to Create:**
1. `src/ui_layer/parsers/pbir_parser.py` - Main PBIR parser
2. `src/ui_layer/parsers/page_parser.py` - Parse page definitions
3. `src/ui_layer/parsers/visual_parser.py` - Parse visual definitions
4. `src/ui_layer/parsers/metadata_formatter.py` - Format raw PBIR data

**Test Files:**
- `tests/unit/test_pbir_parser.py`
- `tests/unit/test_page_parser.py`
- `tests/unit/test_visual_parser.py`

**Success Criteria:**
- Parse complete PBIR folder structure
- Extract all pages and visuals
- Extract data bindings (measures/columns)
- Unit tests pass with sample reports
```

**Why this works:**
- ✅ Specific goal: "Parse PBIR files and extract structure"
- ✅ Lists exact files with full paths
- ✅ Test files specified
- ✅ Measurable success criteria
- ✅ Scope limited (no AI yet - that's Phase 3)

---

### Quick Start - Ready for New Chat
```markdown
## 🚀 Quick Start (For New Chat Session)

**First Prompt in New Chat:**
```
I'm Szabi. I'm starting UI Layer Phase 1 implementation.

Context to load:
1. Read dev2_context.md (current status)
2. Read docs/UI_LAYER_ARCHITECTURE.md (comprehensive architecture)
3. Read docs/tasks/ui_parser_tasks.md (this file - implementation tasks)

Current branch: feature/ui-layer-pbir
Current task: Phase 1 - Core Parsing (PBIRParser, PageParser, VisualParser)

Let's start with Task 1.1: Create PBIRParser class.
```
```

**Why this works:**
- ✅ Complete ready-to-paste prompt
- ✅ Developer identification required (I'm Szabi)
- ✅ Lists all context files to load
- ✅ Specifies branch name
- ✅ Identifies first task clearly
- ✅ New chat can start immediately

---

### Task with Ready-to-Use Prompt
```markdown
## 📅 Phase 1 Implementation Tasks

### Task 1.1: Create PBIRParser (2 hours)
**Goal:** Main parser that coordinates page and visual parsing

**Windsurf Prompt:**
```
Create the main PBIR parser class.

File: src/ui_layer/parsers/pbir_parser.py

Based on docs/UI_LAYER_ARCHITECTURE.md design:
1. Create PBIRParser class that parses PBIR folder structure
2. Implement parse_report() returning ReportStructure
3. Use PageParser and VisualParser for delegation
4. Add error handling for missing/corrupted files
5. Use common.logger for logging

Pattern: Follow src/model_layer/extractors/xmla_extractor.py

Test with: tests/fixtures/sample_reports/minimal_report/
```
```

**Why this works:**
- ✅ Time estimate provided (2 hours)
- ✅ Clear goal statement
- ✅ Complete prompt ready to paste
- ✅ Exact file path specified
- ✅ References architecture doc
- ✅ Lists specific requirements
- ✅ References pattern to follow
- ✅ Specifies test data location

---

## 📚 Example 2: Phase Handoff Document

**Source:** `docs/UI_LAYER_PHASE4_HANDOFF.md` (312 lines)

### Status Summary
```markdown
# UI Layer Phase 4 Handoff - Output Generation

**Created:** November 25, 2025  
**Developer:** Szabi  
**Branch:** `feature/ui-layer-pbir`  
**Status:** Phase 3 COMPLETE ✅ - Ready for Phase 4

---

## 📊 Current Status

### Completed (Phases 1, 2 & 3)

**Phase 1: Core Parsing** ✅
- `PBIRParser` (456 lines) - Main orchestrator
- `PageParser` (217 lines) - Parse pages
- `VisualParser` (387 lines) - Parse visuals and data bindings
- `MetadataFormatter` (344 lines) - Format output
- 13 unit tests, all passing

**Phase 2: Data Binding Analysis** ✅
- `MeasureUsageAnalyzer` (422 lines) - Track measure usage
- `DataBindingAnalyzer` (617 lines) - Column usage, filters, interactions
- 28 unit tests, all passing

**Phase 3: AI Enrichment** ✅
- `PageEnricher` (267 lines) - AI narratives for pages
- `VisualEnricher` (261 lines) - AI descriptions for visuals
- `BatchProcessor` (73 lines) - UI Layer batching
- 2 prompt templates (510 lines)
- 21 unit tests, all passing

**Total Progress:**
- 5 commits on `feature/ui-layer-pbir`
- ~5,300 lines of production code
- 62 unit tests, all passing ✅
- All components < 650 lines
```

**Why this works:**
- ✅ Shows what was already completed (builds confidence)
- ✅ Lists file names and line counts (measurable progress)
- ✅ Shows test counts (quality visible)
- ✅ Aggregate metrics (5,300 lines, 62 tests)
- ✅ Quality standard noted (< 650 lines per file)
- ✅ Everything is ✅ (clear completion status)

---

### Next Phase Goals
```markdown
## 🎯 Phase 4: Output Generation (Next)

### Goal
Generate comprehensive documentation in multiple formats (JSON, Excel, Markdown) 
with statistics and summaries.

### Component to Create

#### **OutputGenerator** (~500 lines)
**File:** `src/ui_layer/generators/output_generator.py`

**Responsibilities:**
- Generate JSON output (complete data structure)
- Generate Excel output (7 sheets with formatted data)
- Generate Markdown output (human-readable documentation)
- Add statistics and summaries
- Format data for readability

**Pattern:** Follow `src/model_layer/generators/output_generator.py`
- Use `openpyxl` for Excel generation
- Use similar sheet structure as Model Layer
- Include formatting (headers, colors, column widths)

**Key Methods:**
```python
def generate(self, report_data: Dict, output_dir: Path) -> Dict[str, Path]:
    """Generate all output formats."""
    
def _generate_json(self, report_data: Dict, output_dir: Path) -> Path:
    """Generate JSON output."""
    
def _generate_excel(self, report_data: Dict, output_dir: Path) -> Path:
    """Generate Excel output with 7 sheets."""
```
```

**Why this works:**
- ✅ Clear goal in 1-2 sentences
- ✅ Estimated file size (~500 lines)
- ✅ Full file path specified
- ✅ Responsibilities listed (what it does)
- ✅ Pattern reference (follow Model Layer)
- ✅ Key methods with signatures (code structure)
- ✅ Specific libraries to use (openpyxl)

---

### Detailed Specifications
```markdown
## 📋 Excel Sheet Structure

### Sheet 1: Summary
- Report name and metadata
- Total pages, visuals, measures used
- Statistics (visual types, measure usage)
- Generation timestamp

### Sheet 2: Pages
- Page name and display name
- Dimensions (width x height)
- Visual count
- Enrichment (purpose, key insights, audience, navigation)
- Measures used on page

### Sheet 3: Visuals
- Visual name and type
- Page name
- Position (x, y, width, height)
- Data bindings (measures, columns)
- Enrichment (purpose, insight, interaction, value)

[... continues for all 7 sheets]
```

**Why this works:**
- ✅ Specific output structure defined
- ✅ Each sheet's content listed
- ✅ Field names specified
- ✅ No ambiguity about what to create
- ✅ AI can implement directly from this

---

### Implementation Steps
```markdown
## 📋 Implementation Steps

### Step 1: Create Generators Folder Structure
```bash
mkdir src/ui_layer/generators
```

Create `src/ui_layer/generators/__init__.py`:
```python
from .output_generator import OutputGenerator

__all__ = ["OutputGenerator"]
```

### Step 2: Create OutputGenerator
1. Copy structure from `src/model_layer/generators/output_generator.py`
2. Adapt for UI Layer data structure
3. Implement 7 Excel sheets (vs 8 in Model Layer)
4. Add UI-specific statistics

### Step 3: Implement JSON Generation
1. Serialize complete report data
2. Include all enrichment data
3. Format for readability (indent=2)
4. Add metadata and timestamps
```

**Why this works:**
- ✅ Step-by-step instructions
- ✅ Includes bash commands
- ✅ Shows code structure
- ✅ References pattern file
- ✅ Notes differences (7 vs 8 sheets)
- ✅ Actionable (developer can follow exactly)

---

## 📚 Example 3: Phase Start Prompt

**Source:** `PHASE4_START_PROMPT.md` (57 lines)

### Complete Structure
```markdown
# 🚀 UI Layer Phase 4 - Start Prompt

**Copy this prompt into your new Windsurf chat to continue:**

---

I'm Szabi. Continue UI Layer Phase 4 implementation.

**Context to load:**
1. Read `dev2_context.md` (current status and session summary)
2. Read `docs/UI_LAYER_ARCHITECTURE.md` (comprehensive architecture)
3. Read `docs/UI_LAYER_PHASE4_HANDOFF.md` (Phase 4 handoff document)

**Current branch:** `feature/ui-layer-pbir`  
**Current status:** Phase 3 COMPLETE ✅ (62 tests passing)

**Phase 3 Completed:**
- ✅ PageEnricher (267 lines) - AI narratives for pages
- ✅ VisualEnricher (261 lines) - AI descriptions for visuals
- ✅ BatchProcessor utility (73 lines)
- ✅ 2 prompt templates (510 lines)
- ✅ 21 unit tests, all passing

**Next task: Phase 4 - Output Generation**

Create `src/ui_layer/generators/output_generator.py`:
- Generate JSON output (complete data structure)
- Generate Excel output (7 sheets with formatted data)
- Generate Markdown output (human-readable documentation)
- Add statistics and summaries

**Pattern to follow:**
- Copy structure from `src/model_layer/generators/output_generator.py`
- Adapt for UI Layer data structure (pages, visuals, enrichment)
- Create 7 Excel sheets (vs 8 in Model Layer)

First, verify branch with: `git branch --show-current`

Then let's start by creating the generators folder structure and OutputGenerator class.

---

## Quick Reference

**What's Done:**
- ✅ Phase 1: Core Parsing (1700+ lines, 13 tests)
- ✅ Phase 2: Data Binding Analysis (2000+ lines, 28 tests)
- ✅ Phase 3: AI Enrichment (1600+ lines, 21 tests)

**What's Next:**
- 📋 Phase 4: Output Generation (600+ lines, 27 tests)

**Key Files to Reference:**
- `src/model_layer/generators/output_generator.py` - Pattern to follow
- `src/ui_layer/enrichers/page_enricher.py` - Data structure
- `.github/copilot-instructions.md` - Coding standards

**Branch:** `feature/ui-layer-pbir` (5 commits, pushed to remote)
```

**Why this works:**
- ✅ Very clear instructions at top (copy this prompt)
- ✅ Complete ready-to-paste section
- ✅ Lists exact context files to load (with paths)
- ✅ Shows current status (Phase 3 complete with metrics)
- ✅ Specific next task clearly stated
- ✅ Pattern file referenced
- ✅ First action specified (verify branch)
- ✅ Quick reference summary
- ✅ Key reference files listed
- ✅ Branch status shown

---

## 📚 Example 4: End-of-Phase Handoff Prompt

**From UI Layer Phase 4 completion:**

```markdown
Phase 4 complete! 🎉

**What was delivered:**
- ✅ OutputGenerator (510 lines, 27 tests)
  - JSON generation working
  - Excel generation (7 sheets, formatted)
  - Markdown generation (human-readable)
- ✅ All 89 tests passing (62 → 89)
- ✅ Branch committed and pushed

**Documentation created for next session:**
- `PHASE5_START_PROMPT.md` - Copy this into new chat
- `docs/UI_LAYER_PHASE5_HANDOFF.md` - Implementation guide
- `dev2_context.md` - Updated with completion

**To start Phase 5 in a new chat:**
Simply copy the contents of `PHASE5_START_PROMPT.md` into a new chat session.
The prompt includes all context files needed and next steps.

**Branch status:** All changes committed and pushed to `feature/ui-layer-pbir`

**Phase 5 preview:**
Next phase will create ReportDocumenter orchestrator (~500 lines) that integrates 
all UI Layer components into a complete pipeline: Parse → Analyze → Enrich → Generate

Ready for Phase 5! 🚀
```

**Why this works:**
- ✅ Celebration (Phase complete!)
- ✅ Specific deliverables listed with metrics
- ✅ Test progression visible (62 → 89)
- ✅ Documentation for next phase clearly listed
- ✅ Instructions for starting next chat
- ✅ Branch status confirmed
- ✅ Preview of next phase (sets expectations)
- ✅ Positive ending (Ready for Phase 5! 🚀)

---

## 📚 Example 5: Task with Code Structure

**From Phase 3 (AI Enrichment):**

```markdown
### Task 3.1: Create PageEnricher (2 hours)
**Goal:** Generate AI narratives for report pages

**Windsurf Prompt:**
```
Create PageEnricher for AI-powered page narratives.

File: src/ui_layer/enrichers/page_enricher.py

Pattern: Follow src/model_layer/enrichers/measure_enricher.py

Implementation:
```python
from typing import Dict, List, Any, Optional
from pathlib import Path
from common.ai_service import AIService
from common.logger import setup_logger
from ..utils.batch_processor import BatchProcessor

class PageEnricher:
    """Enrich page metadata with AI-generated narratives."""
    
    def __init__(self, ai_service: AIService, prompt_path: Path):
        """
        Initialize enricher.
        
        Args:
            ai_service: AI service for generation
            prompt_path: Path to page enrichment prompt template
        """
        self.ai_service = ai_service
        self.prompt_template = self._load_prompt(prompt_path)
        self.logger = setup_logger(__name__)
        
    def enrich_pages(self, pages: List[Dict], report_context: Dict) -> List[Dict]:
        """
        Enrich all pages with AI narratives.
        
        Args:
            pages: List of page metadata from parser
            report_context: Overall report context
            
        Returns:
            List of enriched page metadata
        """
        self.logger.info(f"Enriching {len(pages)} pages")
        
        enriched = []
        for page in pages:
            try:
                enriched_page = self._enrich_single_page(page, report_context)
                enriched.append(enriched_page)
            except Exception as e:
                self.logger.error(f"Failed to enrich page {page['name']}: {e}")
                enriched.append(page)  # Return original on error
                
        return enriched
        
    def _enrich_single_page(self, page: Dict, context: Dict) -> Dict:
        """Enrich single page with AI narrative."""
        prompt = self._build_prompt(page, context)
        response = self.ai_service.generate(prompt)
        enrichment = self._parse_response(response)
        
        return {**page, "enrichment": enrichment}
```

Requirements:
- Load prompt from src/ui_layer/prompts/page_enrichment.md
- Use common.ai_service (already initialized)
- Handle API errors gracefully (return original on error)
- Log progress for each page
- Parse JSON response from AI
- Add type hints and docstrings

Test with: tests/fixtures/sample_reports/minimal_report/
Create: tests/unit/test_page_enricher.py (10+ tests)

Success criteria:
- Enrich sample pages successfully
- Handle API errors without crashing
- Return original page data on error
- Logging shows progress
- 10+ unit tests passing (mocked AI service)
```
```

**Why this works:**
- ✅ Complete class structure provided
- ✅ Method signatures with docstrings
- ✅ Error handling pattern shown
- ✅ Import statements included
- ✅ Type hints used throughout
- ✅ Requirements listed clearly
- ✅ Test requirements specified
- ✅ Success criteria measurable
- ✅ AI can implement directly from this

---

## 🎯 Key Patterns Across All Examples

### 1. Always Specify Exact Paths
```markdown
✅ GOOD: src/ui_layer/parsers/pbir_parser.py
❌ BAD: Create a parser file
```

### 2. Reference Existing Patterns
```markdown
✅ GOOD: Pattern: Follow src/model_layer/extractors/xmla_extractor.py
❌ BAD: Use best practices
```

### 3. Show Code Structure
```markdown
✅ GOOD: [Complete class with method signatures]
❌ BAD: Create methods as needed
```

### 4. Measurable Success Criteria
```markdown
✅ GOOD: 13+ unit tests passing, parse in < 2 seconds
❌ BAD: Make sure it works
```

### 5. Context for New Chats
```markdown
✅ GOOD: Read dev2_context.md, UI_LAYER_ARCHITECTURE.md, PHASE4_HANDOFF.md
❌ BAD: Continue where we left off
```

### 6. Ready-to-Paste Prompts
```markdown
✅ GOOD: [Complete prompt between ``` markers]
❌ BAD: Ask AI to create a parser
```

### 7. Clear Handoffs
```markdown
✅ GOOD: Create PHASE5_START_PROMPT.md, update dev2_context.md
❌ BAD: Just commit and move on
```

---

## 📊 Results from UI Layer Implementation

**Using these patterns resulted in:**
- **5 phases** across 5 separate chat sessions
- **6,335 lines** of production code
- **105 tests** passing (13 → 28 → 49 → 76 → 92 → 105)
- **Zero context degradation** across all phases
- **Consistent code quality** (all files < 650 lines)
- **Developer satisfaction:** *"Very productive, keeping context optimal"*

**Time breakdown:**
- Phase 1: 3-4 hours
- Phase 2: 3-4 hours
- Phase 3: 3-4 hours
- Phase 4: 2-3 hours
- Phase 5: 2-3 hours
- **Total:** ~15 hours over 5 days

**Key success factors:**
1. Each phase had clear deliverables
2. Tests required before moving on
3. Handoff docs created for each phase
4. Start prompts ready to paste
5. Code examples in every task
6. References to existing patterns
7. Context efficiently managed

---

**These patterns work. Copy them!**
