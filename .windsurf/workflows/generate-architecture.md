# Generate Architecture Workflow

Create or update SOLUTION_ARCHITECTURE.md for a project.

---

## When to Use

- **New project:** Define structure before coding
- **Existing project:** Document current structure
- **Major refactor:** Update after significant changes

---

## Mode A: Analyze Existing Project

### Step 1: Scan Project Structure

```bash
# Get directory tree
find . -type f -name "*.py" -o -name "*.js" -o -name "*.ts" | head -50
ls -la
```

### Step 2: Identify Key Patterns

Look for:
- Source code location (`src/`, `lib/`, `app/`)
- Test location (`tests/`, `__tests__/`, `spec/`)
- Configuration files
- Entry points (`main.py`, `index.js`, `app.py`)
- Package/module structure

### Step 3: Ask Clarifying Questions

```
I've scanned the project. Let me confirm:

1. Main source code is in: {location}?
2. Tests are in: {location}?
3. The project is a: {type - API, CLI, library, etc}?
4. Main language(s): {languages}?
5. Any special conventions I should know about?
```

### Step 4: Generate Document

Create `SOLUTION_ARCHITECTURE.md` using template from `.ai/templates/SOLUTION_ARCHITECTURE_TEMPLATE.md`

---

## Mode B: Design New Project

### Step 1: Gather Requirements

```
Let's design the project structure. Please tell me:

1. What does this project do? (brief description)
2. What type of project? (API, CLI, library, web app, etc)
3. Main language(s)?
4. Any specific frameworks? (FastAPI, React, etc)
5. Expected size? (small script, medium app, large system)
6. Will it have tests? What kind?
7. Any deployment considerations?
```

### Step 2: Propose Structure

Based on answers, propose a structure:

```markdown
## Proposed Structure

{project}/
├── src/                    # Source code
│   ├── {module1}/          # {purpose}
│   ├── {module2}/          # {purpose}
│   └── common/             # Shared utilities
├── tests/                  # Test files
│   ├── unit/
│   └── integration/
├── config/                 # Configuration
├── docs/                   # Documentation
│   ├── tasks/              # Task files (AI workflow)
│   └── ...
└── scripts/                # Utility scripts

Does this structure work for you, or should we adjust?
```

### Step 3: Confirm and Generate

After user confirms, create `SOLUTION_ARCHITECTURE.md`

---

## Document Structure

The generated `SOLUTION_ARCHITECTURE.md` should include:

1. **Overview** - What the project does
2. **Directory Structure** - Full tree with descriptions
3. **Components** - Key modules/packages and their responsibilities
4. **File Placement Rules** - Where different file types go
5. **Naming Conventions** - How to name files, classes, etc.
6. **Dependencies** - Key external dependencies
7. **Configuration** - How config is handled

---

## Template Reference

See `.ai/templates/SOLUTION_ARCHITECTURE_TEMPLATE.md` for full template.

---

## Tips

### Keep It Updated
- Update when adding new modules
- Update after major refactors
- Keep file placement rules current

### Be Specific
- Include actual paths, not just patterns
- Give concrete examples for naming
- List real dependencies

### Link to Standards
Reference `.ai/standards/{language}.md` for coding standards rather than duplicating.

---

## Example Output

```markdown
# Solution Architecture

## Overview
PowerBI Documentation Suite - Multi-layer documentation generator.

## Structure
project/
├── src/
│   ├── sql_layer/      # Database documentation
│   ├── model_layer/    # Semantic model docs
│   ├── ui_layer/       # Report UI docs
│   └── common/         # Shared utilities
├── tests/
│   ├── unit/           # Fast unit tests
│   └── integration/    # Full pipeline tests
├── config/
│   └── config.yaml     # Main configuration
├── docs/
│   ├── tasks/          # AI task files
│   └── architecture/   # Design docs
└── output/             # Generated documentation

## File Placement
| Type | Location |
|------|----------|
| Source code | src/{layer}/ |
| Unit tests | tests/unit/{layer}/ |
| Integration tests | tests/integration/ |
| Task files | docs/tasks/ |
| Config | config/ |

## Naming Conventions
- Files: snake_case.py
- Classes: PascalCase
- Tests: test_{module}.py
```
