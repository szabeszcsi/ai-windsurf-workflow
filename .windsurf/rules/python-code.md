---
trigger: glob
globs: ["**/*.py"]
description: Python Development Standards (Source & Test)
---
# Python Master Rule

**Scope:** Applies to ALL Python files (Source AND Tests).

## 1. THE GOLDEN RULE OF TESTING
**You are FORBIDDEN from finishing a coding task without running tests.**
**⚠️ NEVER change working source code just to make tests pass.**
- **Edit Source** → **Run Test** → **Fix** → **Verify**.
- If tests don't exist, **CREATE THEM** in `tests/unit/{module}/`.
- **Target:** 80% coverage minimum.

## 2. CONTEXT AWARENESS (Read Before Write)
Before editing `src/{layer}/{module}.py`:
1. Check for `docs/tech-summaries/{layer}/{module}.md`.
2. If it exists, **READ IT**.
3. If it doesn't exist, read the source file directly AND DISCLOSE to user: tech summary is not complete, recommend: `/generate-tech-summary`
4. Read `SOLUTION_ARCHITECTURE.md` (if exists)

## 3. FILE STRUCTURE & LIMITS
- **Location:** `src/{layer}/{module}.py` (Mirror: `tests/unit/{layer}/test_{module}.py`)
- **Limits:** Max 500 lines per file (Split if exceeded). Max 50 lines per function.
- **Imports:**
  - ✅ Absolute: `from src.common.utils import helper`
  - ❌ Relative: `from ..utils import helper` (FORBIDDEN in `src/`)
  - Order: Standard library, third party, project imports

## 4. CODING STANDARDS (Required Patterns)

### Type Hints & Docstrings
```python
def process(self, data: list[dict]) -> dict[str, Any]:
    """Brief description (Google Style).
    
    Args:
        data: Input description
    Returns:
        Output description
    """
    pass
```

### Logging
```python
import logging
logger = logging.getLogger(__name__)
# Use logger.info(), logger.error(f"Msg: {e}", exc_info=True)
```

### Error Handling
- ✅ Catch specific exceptions (`ValueError`, `FileNotFoundError`).
- ✅ Log with `exc_info=True`.
- ❌ NEVER use bare `except:`.

## 5. TESTING REQUIREMENTS (Strict Gate)
**When creating or modifying behavior:**
1. **Create/Update Test:** `tests/unit/{module}/test_{filename}.py` Filename pattern: `{what}_{condition}_{expected}`
2. **Cover:** Happy path, Edge cases, Error handling.
3. **Mock:** External services (DB, API) must be mocked.
4. **Run:** `pytest tests/unit/{module}/ -v`

**Do not skip tests.** Code without tests is incomplete.

## 6. Naming

| Element | Convention | Example |
|---------|------------|---------|
| Files | snake_case | `data_processor.py` |
| Classes | PascalCase | `DataProcessor` |
| Functions | snake_case | `process_data()` |
| Constants | UPPER_SNAKE | `MAX_RETRIES` |

## 7. Don'ts

| Don't | Do Instead |
|-------|------------|
| Hardcode config | Use config files |
| Hardcode secrets | Use env vars or credentials file |
| Skip error handling | Wrap risky operations |
| Duplicate code | Check existing utilities, sources first |
