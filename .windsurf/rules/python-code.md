---
trigger: glob
globs: ["**/*.py", "!**/test_*.py", "!**/*_test.py", "!**/tests/**/*.py"]
description: Python coding standards for source files (not tests)
---

# Python Code Standards

**Full reference:** `.ai/standards/python.md`

---

## File Limits

| Metric | Limit |
|--------|-------|
| Lines per file | 500 max (650 hard limit) |
| Lines per function | 50 max |
| Nesting depth | 4 levels max |

**If exceeded:** Split into logical modules.

---

## Required Patterns

```python
# Logging - use project logger or standard
import logging
logger = logging.getLogger(__name__)

# Type hints on public methods
def process(self, data: list[dict]) -> dict[str, Any]:
    ...

# Docstrings (Google style)
def calculate(items: list, rate: float) -> float:
    """Brief description.

    Args:
        items: What this parameter is
        rate: What this parameter is

    Returns:
        What gets returned
    """
```

---

## Naming Conventions

| Element | Convention | Example |
|---------|------------|---------|
| Files | snake_case | `data_processor.py` |
| Classes | PascalCase | `DataProcessor` |
| Functions | snake_case | `process_data()` |
| Constants | UPPER_SNAKE | `MAX_RETRIES` |
| Private | _prefix | `_internal_method()` |

---

## Import Order

```python
# 1. Standard library
import os
from pathlib import Path

# 2. Third-party
import pandas as pd

# 3. Project imports
from src.common import utils
```

---

## Error Handling

```python
# ✅ Specific exceptions with context
try:
    result = parse_config(path)
except FileNotFoundError:
    logger.error(f"Config not found: {path}")
    raise
except json.JSONDecodeError as e:
    logger.error(f"Invalid JSON in {path}: {e}")
    raise

# ❌ Never do this
try:
    something()
except:
    pass
```

---

## Common Pitfalls

```python
# ❌ Mutable default argument
def add_item(item, items=[]):
    items.append(item)
    return items

# ✅ Use None
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items
```

---

## Configuration-Driven Development

```python
# ✅ Configuration-driven
config = load_config()
model = config.get('ai_model', 'default-model')
timeout = config.get('timeout', 30)

# ❌ Hardcoded
model = "gpt-4"
timeout = 30
```

---

## Universal Don'ts

| Don't | Do Instead |
|-------|------------|
| Hardcode config values | Use config files (YAML, JSON, env) |
| Hardcode API keys/secrets | Use credentials file or env vars (never commit!) |
| Skip error handling | Wrap risky operations (API calls, DB, file I/O) |
| Duplicate code | Check for existing utilities first |
| Ignore shared modules | Use project's common/ utilities |
| Commit secrets/logs | Ensure `.gitignore` covers them |