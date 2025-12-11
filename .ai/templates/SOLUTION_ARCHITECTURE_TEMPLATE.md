# Solution Architecture

<!-- 
This file defines YOUR PROJECT's structure.
Generate with /generate-architecture or create manually.
Update when structure changes significantly.
-->

## Overview

{Brief description of what this project does - 2-3 sentences}

**Type:** {API / CLI / Library / Web App / etc.}  
**Primary Language:** {Python / JavaScript / etc.}  
**Framework:** {FastAPI / React / None / etc.}

---

## Directory Structure

```
{project}/
├── src/                        # Source code
│   ├── {component1}/           # {Description}
│   ├── {component2}/           # {Description}
│   └── common/                 # Shared utilities
│
├── tests/                      # Test files
│   ├── unit/                   # Fast unit tests
│   │   └── {component}/        # Tests for each component
│   └── integration/            # Full pipeline tests
│
├── config/                     # Configuration files
│   └── config.yaml             # Main configuration
│
├── docs/                       # Documentation
│   ├── tasks/                  # AI task files & handoffs
│   │   └── completed/          # Archived handoffs
│   ├── working/                # Work-in-progress docs
│   └── archive/                # Archived sessions
│
├── scripts/                    # Utility scripts
│
├── .ai/                        # AI workflow system
├── .claude/commands/           # Slash commands
├── .devcontainer/              # Dev container config
│
├── CLAUDE.md                   # AI entry point
├── SOLUTION_ARCHITECTURE.md    # This file
├── dev_context.md              # Session state
└── {main entry point}          # main.py, index.js, etc.
```

---

## Components

### {Component 1}
**Location:** `src/{component1}/`  
**Purpose:** {What this component does}  
**Key Files:**
- `{file1}.py` - {Description}
- `{file2}.py` - {Description}

### {Component 2}
**Location:** `src/{component2}/`  
**Purpose:** {What this component does}

### Common/Shared
**Location:** `src/common/`  
**Purpose:** Utilities shared across components
- `config.py` - Configuration loading
- `logger.py` - Logging setup
- `utils.py` - General utilities

---

## File Placement Rules

| File Type | Location | Example |
|-----------|----------|---------|
| Source code | `src/{component}/` | `src/api/routes.py` |
| Unit tests | `tests/unit/{component}/` | `tests/unit/api/test_routes.py` |
| Integration tests | `tests/integration/` | `tests/integration/test_full_pipeline.py` |
| Task files | `docs/tasks/` | `docs/tasks/api_tasks.md` |
| Handoffs | `docs/tasks/` | `docs/tasks/api_phase2_handoff.md` |
| WIP docs | `docs/working/` | `docs/working/bug_investigation.md` |
| Config | `config/` | `config/config.yaml` |
| Scripts | `scripts/` | `scripts/setup.sh` |

**Never create files in project root** except:
- `CLAUDE.md`, `SOLUTION_ARCHITECTURE.md`, `dev_context.md`
- Main entry point (`main.py`, `index.js`)
- Standard config files (`.gitignore`, `requirements.txt`, `package.json`)

---

## Naming Conventions

| Element | Convention | Example |
|---------|------------|---------|
| Python files | snake_case | `data_processor.py` |
| Python classes | PascalCase | `DataProcessor` |
| Test files | test_*.py | `test_data_processor.py` |
| Config files | lowercase | `config.yaml` |
| Docs | UPPER_SNAKE or Title | `ARCHITECTURE.md` |

---

## Dependencies

### Runtime
- {package1} - {purpose}
- {package2} - {purpose}

### Development
- pytest - Testing
- {linter} - Code quality

---

## Configuration

**Main config:** `config/config.yaml`

```yaml
# Example structure
app:
  name: "{project name}"
  debug: false

database:
  host: "localhost"
  port: 5432

# etc.
```

**Secrets:** Use environment variables or `config/credentials.yaml` (gitignored)

---

## Entry Points

| Purpose | Command |
|---------|---------|
| Run main app | `python main.py` |
| Run tests | `pytest tests/` |
| Run specific test | `pytest tests/unit/test_something.py` |

---

## Notes

{Any project-specific notes, conventions, or decisions that don't fit above}

---

*Last updated: {date}*
