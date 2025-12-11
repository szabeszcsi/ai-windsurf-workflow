# AI Agent System Reference

**Purpose:** Framework architecture reference for extension and deep troubleshooting

**When to read this:**
- Adding new language support
- System behavior unclear (after workflows haven't helped)
- Debugging why files aren't loading
- Understanding the two-tier architecture

**Don't read this for:**
- Normal session start (use `/start-session`)
- Saving progress (use `/update-context`)
- Context confusion (use `/reload-context` first)

---

## Architecture: Two-Tier Documentation System

This framework uses **lazy loading** for documentation to optimize token usage.

### Tier 1: Auto-Triggered Rules (`.windsurf/rules/`)

**Purpose:** Condensed summaries loaded automatically by Windsurf

**Characteristics:**
- **Size:** ~100-150 lines (token-optimized)
- **Trigger:** File glob patterns
- **Loading:** Automatic when editing matching files
- **Content:** Essential patterns, limits, quick reference

**Example:**
```yaml
# .windsurf/rules/python-code.md
---
trigger: glob
globs: ["**/*.py", "!**/test_*.py", "!**/*_test.py", "!**/tests/**/*.py"]
---
# Python Code Standards
**Full reference:** `.ai/standards/python.md`
[... condensed patterns ...]
```

### Tier 2: Full Standards (`.ai/standards/`)

**Purpose:** Complete reference documentation

**Characteristics:**
- **Size:** ~250+ lines (comprehensive)
- **Trigger:** Manual/on-demand (see core-rules "Load On Demand" table)
- **Loading:** Explicit read when deeper detail needed
- **Content:** Detailed examples, edge cases, full explanations

**Example:**
```markdown
# .ai/standards/python.md
# Python Coding Standards

## Required in Every File
[... detailed patterns with examples ...]

## Error Handling
[... comprehensive guide ...]

## Common Pitfalls
[... full examples ...]
```

### Why Two Tiers?

**Token Efficiency:**
- Auto-load small summaries (~143 lines) instead of full docs (~257 lines)
- **40%+ token savings** per file edit
- Scales to 30k-40k tokens saved over 100 edits

**Separation of Concerns:**
- `.windsurf/rules/` = Windsurf-specific auto-triggers
- `.ai/standards/` = Tool-agnostic reference docs
- Easy to port to other AI IDEs

**Multi-Language Ready:**
- Pattern: `{language}-code.md` (rule) + `{language}.md` (standard)
- Currently: Python + Testing
- Extensible: JavaScript, SQL, DAX, etc.

---

## File Reference Map

### Project Root Files

| File | Purpose | Load When |
|------|---------|-----------|
| `dev_context.md` | Single-dev session state | Every `/start-session` |
| `dev{N}_context.md` | Multi-dev session state (N=1,2,3...) | `/start-session` (based on team.md) |
| `PROJECT_STATUS.md` | Project overview | `/start-session` (optional) |
| `SOLUTION_ARCHITECTURE.md` | Project structure | `/start-session`, `/plan-task` |
| `FRAMEWORK_SETUP.md` | Human setup guide | Never (human-facing) |

### `.windsurf/` Structure

| Path | Purpose | Trigger |
|------|---------|---------|
| `rules/core-rules.md` | Always-on core behaviors | `always_on` |
| `rules/team.md` | Multi-dev configuration | Referenced by workflows |
| `rules/python-code.md` | Python standards summary | `**/*.py` (non-test) |
| `rules/python-tests.md` | Testing standards summary | `**/test_*.py`, `**/*_test.py` |
| `workflows/*.md` | Executable workflows | `/workflow-name` command |

### `.ai/` Structure

| Path | Purpose | Load When |
|------|---------|-----------|
| `AGENT_REFERENCE.md` | This file - system reference | System unclear, adding languages |
| `standards/python.md` | Full Python standards | Writing Python (on-demand) |
| `standards/testing.md` | Full testing standards | Writing tests (on-demand) |
| `templates/HANDOFF_TEMPLATE.md` | Phase handoff template | Creating handoffs |
| `templates/TASK_FILE_TEMPLATE.md` | Task planning template | `/plan-task` workflow |
| `templates/SOLUTION_ARCHITECTURE_TEMPLATE.md` | Architecture template | `/generate-architecture` |

### `docs/` Structure

| Path | Purpose | Created By |
|------|---------|------------|
| `docs/tasks/{name}_tasks.md` | Task definition | `/plan-task` |
| `docs/tasks/{name}_phase{N}_handoff.md` | Phase instructions | `/phase-complete` (previous phase) |
| `docs/tasks/{name}_phase{N}_complete.md` | Phase completion record | `/phase-complete` |
| `docs/tasks/completed/` | Archived handoffs | `/phase-complete` |
| `docs/working/` | Work-in-progress docs | Ad-hoc |
| `docs/archive/` | Old sessions | Manual archive |
| `docs/tech-summaries/{layer}/{module}.md` | Module API summaries | `/generate-tech-summary` |

---

## Multi-Developer Detection

### How to Detect Multi-Dev Project

```python
if file_exists('.windsurf/team.md'):
    # Multi-developer project
    ask_user("Who are you?")
    load_context_from_team_mapping()
else:
    # Single-developer project
    load('dev_context.md')
```

### Team Configuration Format

`.windsurf/team.md` contains:

```markdown
## Developers

| ID | Name | Context File | Primary Domain |
|----|------|--------------|----------------|
| 1  | Alice | dev1_context.md | Backend |
| 2  | Bob   | dev2_context.md | Frontend |
```

**Workflow:**
1. Check if `.windsurf/team.md` exists
2. If yes: Ask "WHO ARE YOU?"
3. User responds: "Alice" or "1"
4. Load corresponding context file: `dev1_context.md`

---

## Adding New Language Support

### Step-by-Step Process

**Example: Adding JavaScript support**

### 1. Create Full Standard

File: `.ai/standards/javascript.md`

```markdown
# JavaScript Coding Standards

## Required in Every File
- ESLint configuration
- Proper imports/exports
- JSDoc comments for public functions

## Naming Conventions
| Element | Convention | Example |
|---------|------------|---------|
| Files | kebab-case | `data-processor.js` |
| Classes | PascalCase | `DataProcessor` |
| Functions | camelCase | `processData()` |
| Constants | UPPER_SNAKE | `MAX_RETRIES` |

## Import Order
1. Node built-ins
2. Third-party packages
3. Project imports

## Error Handling
[... comprehensive examples ...]

## Common Pitfalls
[... detailed patterns ...]
```

**Size target:** ~250+ lines with examples

### 2. Create Condensed Rule

File: `.windsurf/rules/javascript-code.md`

```markdown
---
trigger: glob
globs: ["**/*.js", "**/*.jsx", "!**/*.test.js", "!**/*.spec.js"]
description: JavaScript coding standards
---

# JavaScript Code Standards

**Full reference:** `.ai/standards/javascript.md`

---

## File Limits
| Metric | Limit |
|--------|-------|
| Lines per file | 500 max |
| Lines per function | 50 max |

## Required Patterns
- Use ESLint
- Modern ES6+ syntax
- Async/await over callbacks
- JSDoc on public functions

## Naming Conventions
[... condensed table ...]

## Error Handling
[... key patterns only ...]
```

**Size target:** ~150 lines maximum

**Critical:** Must include reference to full standard:
```markdown
**Full reference:** `.ai/standards/javascript.md`
```

### 3. Update Core Rules

Add to `.windsurf/rules/core-rules.md` in "Load On Demand" section:

```markdown
| Writing JavaScript | `.ai/standards/javascript.md` |
```

### 4. Update Templates (Optional)

Templates already use `{language}` placeholder, so usually no changes needed.

Only update if adding language-specific sections.

### 5. Test

1. Create a `.js` file in the project
2. Verify auto-load of `javascript-code.md`
3. Check AI follows JavaScript conventions
4. Verify AI can read full standard when needed

---

## File Loading Decision Tree

```
User edits file
    ↓
Is it a Python file (*.py, non-test)?
    YES → Auto-load .windsurf/rules/python-code.md
    NO  → Continue
    ↓
Is it a Python test file?
    YES → Auto-load .windsurf/rules/python-tests.md
    NO  → Continue
    ↓
Is it a JavaScript file?
    YES → Auto-load .windsurf/rules/javascript-code.md (if exists)
    NO  → Continue
    ↓
(Add more language patterns as needed)
```

**Edge Case: conftest.py**

Test configuration files like `conftest.py` (pytest) or `test_helper.py`:
- **Trigger:** Only `python-code.md` (not `python-tests.md`)
- **Reason:** Filename doesn't match `test_*.py` or `*_test.py` pattern
- **Behavior:** Treated as regular Python file, which is correct
- **Note:** If you need test-specific guidance for conftest.py, reference `.ai/standards/testing.md` manually

```
AI needs detailed information
    ↓
Check core-rules.md "Load On Demand" table
    ↓
Find matching scenario:
    - Writing Python → Read .ai/standards/python.md
    - Writing tests → Read .ai/standards/testing.md
    - Creating handoff → Read .ai/templates/HANDOFF_TEMPLATE.md
    - System unclear → Read .ai/AGENT_REFERENCE.md (this file)
    ↓
Load specified file
```

---

## Maintaining Sync Between Tiers

**Critical:** When updating standards, sync both files.

### Update Process

1. **Update full standard first:**
   - Edit `.ai/standards/{language}.md`
   - Add new patterns, examples, conventions
   - Update existing guidance

2. **Update condensed rule:**
   - Edit `.windsurf/rules/{language}-code.md`
   - Add ONLY critical new patterns to summary
   - Keep concise - point to full standard for details

3. **Verify reference:**
   - Ensure rule file still has: `**Full reference:** .ai/standards/{language}.md`

### What Goes in Each Tier?

**Full Standard (`.ai/standards/`):**
- ✅ Comprehensive examples
- ✅ Edge cases and pitfalls
- ✅ Detailed explanations
- ✅ Context and reasoning
- ✅ Multiple approaches

**Condensed Rule (`.windsurf/rules/`):**
- ✅ File/function limits
- ✅ Essential patterns
- ✅ Quick reference tables
- ✅ Critical don'ts
- ❌ No detailed examples (reference full standard)
- ❌ No edge cases (reference full standard)

---

## Self-Diagnosis: When Workflows Aren't Enough

**If you've tried workflows and still confused:**

### Symptoms Checklist

- [ ] Re-reading files already read this session
- [ ] Asking questions already answered
- [ ] Can't find expected files
- [ ] Confused about file structure
- [ ] Uncertain about multi-dev vs single-dev
- [ ] Don't know which standard to load

### Recovery Steps

**1. Check if multi-dev project:**
```bash
ls .windsurf/team.md
```
- Exists → Multi-dev, load dev{N}_context.md based on user
- Not exists → Single-dev, load dev_context.md

**2. Verify core files exist:**
```bash
ls dev_context.md
ls PROJECT_STATUS.md
ls SOLUTION_ARCHITECTURE.md
```

**3. Check file mapping:**
- Use the "File Reference Map" section above
- Verify files are in expected locations

**4. Review load-on-demand table:**
- Read `.windsurf/rules/core-rules.md`
- Section: "📂 Load On Demand"
- Match your scenario to action

**5. If still unclear:**
- This is rare - workflows handle 99% of cases
- Consider asking user for clarification
- May indicate framework misconfiguration

---

## Design Principles

Understanding these helps when extending the framework:

1. **Explicit over implicit**
   - Clear file names (`python-code.md`, not `py.md`)
   - Obvious locations (`standards/`, not `std/`)
   - Direct references (full paths, not abbreviations)

2. **Lazy loading**
   - Load small summaries automatically
   - Load full docs on-demand
   - Optimize for common case (90% of edits)

3. **Context preservation**
   - Session state in dev_context files
   - Task Constants prevent breaking changes
   - Handoffs preserve context across phases

4. **Token efficiency**
   - Two-tier documentation saves 40%+ tokens
   - Minimal auto-loaded content
   - Comprehensive when needed

5. **Multi-developer ready**
   - Isolated contexts per developer
   - Team configuration support
   - Coordination through handoffs

---

## When to Read This File

**DO read when:**
- ✅ Adding new language support
- ✅ Understanding two-tier architecture
- ✅ Debugging file loading issues
- ✅ Extending the framework
- ✅ Workflows haven't resolved confusion

**DON'T read when:**
- ❌ Starting new session (use `/start-session`)
- ❌ Saving progress (use `/update-context`)
- ❌ Context confused (try `/reload-context` first)
- ❌ Phase complete (use `/phase-complete`)
- ❌ Normal workflow scenarios (workflows handle these)

---

*This is a reference document, not a runtime guide. Workflows handle 99% of scenarios.*
