---
trigger: glob
globs: ["**/*.py", "!**/test_*.py", "!**/*_test.py"]
description: Python coding standards - automatically loaded when working with Python source files
---

# Python Coding Standards

## 🚨 After Every Code Change

**CRITICAL:** Update `docs/tech-summaries/{layer}/{module}.md`

**Include:**
- Public function/method signatures
- Class constructors & public methods
- Dependencies (uses/used by)
- Key design patterns

**Template:** `.ai/templates/TECH_SUMMARY_TEMPLATE.md`

**Why:** Multi-session continuity - fresh chats load summaries (2KB) vs full source (50KB)

---

## File Limits

| Metric | Limit |
|--------|-------|
| Lines per file | 500-650 max |
| Lines per function/method | 50 max |

**If exceeded:** Split into logical modules.

---

## Required in Every File

```python
# Logging
from common.logger import setup_logger  # or: import logging
logger = setup_logger(__name__)

# Type hints on public methods
def process(self, data: List[Dict]) -> Dict[str, Any]:
    ...

# Docstrings (Google style)
"""Brief description.

Args:
    data: Input data description

Returns:
    Output description
"""
```

---

## Naming Conventions

| Element | Convention | Example |
|---------|------------|---------|
| Files | snake_case | `data_processor.py` |
| Classes | PascalCase | `DataProcessor` |
| Functions | snake_case | `process_data()` |
| Variables | snake_case | `user_count` |
| Constants | UPPER_SNAKE | `MAX_RETRIES` |
| Private | _prefix | `_internal_method()` |

---

## Import Order

```python
# 1. Standard library
import os
import sys
from pathlib import Path

# 2. Third-party packages
import pandas as pd
from sqlalchemy import create_engine

# 3. Project imports
from common.config import Config
from .utils import helper_function
```

---

## Error Handling

```python
# ✅ DO: Catch specific exceptions
try:
    result = parse_config(path)
except FileNotFoundError:
    logger.error(f"Config file not found: {path}")
    raise
except json.JSONDecodeError as e:
    logger.error(f"Invalid JSON: {e}")
    raise

# ❌ DON'T: Bare except or swallow errors
try:
    risky_operation()
except:  # BAD
    pass  # BAD
```

---

## Type Hints

```python
from typing import List, Dict, Optional, Union, Any

def process(items: List[str]) -> Dict[str, int]:
    ...

def find_user(id: int) -> Optional[User]:
    ...
```

---

## Common Pitfalls

```python
# ❌ Mutable default argument
def add_item(item, items=[]):  # BAD
    items.append(item)
    return items

# ✅ Use None instead
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items
```
