---
name: generate-architecture
description: Create SOLUTION_ARCHITECTURE.md from requirements. Run when starting a new project.
auto_execution_mode: 0
---

# Generate Architecture

Create or update `SOLUTION_ARCHITECTURE.md` from requirements/SOW.

**Use when:**
- Starting a new project
- Major architectural changes
- Onboarding to existing project (document what exists)

---

## Step 1: Gather Requirements

**What input do you have?**

| Input Type | Examples |
|------------|----------|
| SOW / Requirements doc | Formal specification |
| Scoping call transcript | Meeting notes, discussion |
| User description | Verbal/written explanation |
| Existing codebase | Reverse-engineer structure |

**Ask if unclear:**
```
To create the architecture, I need to understand:

1. What does this project do? (brief description)
2. What type? (API, CLI, library, web app, etc.)
3. Main language(s) and frameworks?
4. Key components/modules?
5. External dependencies? (databases, APIs, services)
6. Expected scale? (small script → large system)
7. Any constraints? (security, performance, compliance)
```

---

## Step 2: Analyze Requirements

From input, extract:

### Core Purpose
- What problem does it solve?
- Who uses it?
- What's the main workflow?

### Technical Decisions
- Language(s) and version(s)
- Frameworks
- Database/storage
- External integrations

### Component Breakdown
- What are the main modules?
- How do they interact?
- What are the boundaries?

---

## Step 3: Propose Structure

Based on analysis, create directory structure:

```markdown
## Proposed Structure

{project}/
├── src/                    # Source code
│   ├── {component1}/       # {purpose}
│   ├── {component2}/       # {purpose}
│   └── common/             # Shared utilities
│
├── tests/                  # Test files
│   ├── unit/               # Fast, isolated tests
│   └── integration/        # Full pipeline tests
│
├── config/                 # Configuration
│   └── config.yaml         # Main config
│
├── docs/                   # Documentation
│   ├── tasks/              # Task files for AI workflow
│   │   └── completed/      # Archived handoffs
│   ├── tech-summaries/     # Module API summaries
│   │   └── {layer}/        # Per-layer summaries
│   └── working/            # Work-in-progress
│
├── scripts/                # Utility scripts
│
├── .windsurf/              # Windsurf configuration
│   ├── rules/              # Coding rules
│   ├── workflows/          # Workflow definitions
│   └── team.md             # Developer mapping
│
├── SOLUTION_ARCHITECTURE.md  # This file
├── PROJECT_STATUS.md         # Current status
├── dev_context.md            # Session state
└── {entry_point}             # main.py, index.js, etc.
```

**Confirm with user:**
```
Does this structure work for your project?
[Y] Yes, generate architecture doc
[M] Modify structure first
[?] Questions about specific choices
```

---

## Step 4: Generate SOLUTION_ARCHITECTURE.md

Create the file using template from `.ai/templates/SOLUTION_ARCHITECTURE_TEMPLATE.md`

**Key sections:**

```markdown
# Solution Architecture

## Overview
{Brief description - 2-3 sentences}

**Type:** {API / CLI / Library / Web App / etc.}
**Primary Language:** {language}
**Framework:** {framework or "None"}

---

## Directory Structure
{Full tree with descriptions}

---

## Components

### {Component 1}
**Location:** `src/{component1}/`
**Purpose:** {what it does}
**Key Files:**
- `{file}.py` - {description}

### {Component 2}
...

---

## File Placement Rules

| File Type | Location | Example |
|-----------|----------|---------|
| Source code | `src/{component}/` | `src/api/routes.py` |
| Unit tests | `tests/unit/{component}/` | `tests/unit/api/test_routes.py` |
| Tech summaries | `docs/tech-summaries/{layer}/` | `docs/tech-summaries/api/routes.md` |
| Task files | `docs/tasks/` | `docs/tasks/api_tasks.md` |

---

## Dependencies

### Runtime
- {package} - {purpose}

### Development
- pytest - Testing
- {linter} - Code quality

---

## Configuration

**Main config:** `config/config.yaml`
**Secrets:** Environment variables or `config/credentials.yaml` (gitignored)

---

## Entry Points

| Purpose | Command |
|---------|---------|
| Run app | `python main.py` |
| Run tests | `pytest tests/` |
```

---

## Step 5: Initialize Tech Summaries Structure

Create initial structure:

```bash
mkdir -p docs/tech-summaries
```

Create `docs/tech-summaries/_index.md`:

```markdown
# Tech Summaries

Quick reference documentation for each module.
Load these (~2KB each) instead of full source (~50KB) for faster context.

## Layers

| Layer | Modules | Status |
|-------|---------|--------|
| {layer1} | {planned modules} | 📋 Planned |
| {layer2} | {planned modules} | 📋 Planned |

## Usage

- Before implementing: Read relevant summaries
- After implementing: Update via `/phase-complete`
- If stale: Run `/generate-tech-summary --validate`
```

---

## Step 6: Confirm Output

```
✅ ARCHITECTURE GENERATED

Created:
- SOLUTION_ARCHITECTURE.md ({N} lines)
- docs/tech-summaries/_index.md

Next steps:
1. Review and adjust SOLUTION_ARCHITECTURE.md
2. Create PROJECT_STATUS.md (optional)
3. Create dev_context.md from template
4. Start first task with /plan-task
```

---

## Modes

### New Project (default)
- Full requirements gathering
- Create from scratch

### Document Existing
```
/generate-architecture --existing
```
- Scan existing codebase
- Generate architecture from what exists
- Fill in gaps with questions

### Update
```
/generate-architecture --update
```
- Read existing SOLUTION_ARCHITECTURE.md
- Update specific sections
- Preserve what's still accurate

---

## Quick Reference

| Input | Output |
|-------|--------|
| Requirements/SOW | `SOLUTION_ARCHITECTURE.md` |
| Scoping discussion | Project structure |
| Existing codebase | Documentation of what exists |

**After architecture:**
→ Use `/plan-task` for each feature
→ Use `/phase-complete` to update tech summaries