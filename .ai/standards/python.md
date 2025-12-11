# Python Coding Standards

Python-specific conventions and patterns.

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
def calculate_total(items: List[Item], tax_rate: float) -> float:
    """Calculate total price including tax.

    Args:
        items: List of items to total
        tax_rate: Tax rate as decimal (e.g., 0.08 for 8%)

    Returns:
        Total price including tax

    Raises:
        ValueError: If tax_rate is negative
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

Use absolute imports for project code. Relative imports only within same package.

---

## Type Hints

```python
# Basic types
def greet(name: str) -> str:
    return f"Hello, {name}"

# Collections
from typing import List, Dict, Optional, Union, Any

def process(items: List[str]) -> Dict[str, int]:
    ...

# Optional (can be None)
def find_user(id: int) -> Optional[User]:
    ...

# Union (multiple types)
def parse(value: Union[str, int]) -> str:
    ...

# Type aliases for complex types
ResultDict = Dict[str, List[Tuple[int, str]]]

def analyze(data: ResultDict) -> None:
    ...
```

---

## Classes

```python
class DataProcessor:
    """Process data from various sources.
    
    Attributes:
        config: Configuration settings
        logger: Logger instance
    """

    def __init__(self, config: Config) -> None:
        """Initialize processor.
        
        Args:
            config: Configuration settings
        """
        self.config = config
        self.logger = setup_logger(__name__)
        self._cache: Dict[str, Any] = {}

    def process(self, data: List[Dict]) -> Dict[str, Any]:
        """Process data and return results."""
        self.logger.info(f"Processing {len(data)} items")
        try:
            result = self._transform(data)
            return result
        except ProcessingError as e:
            self.logger.error(f"Processing failed: {e}")
            raise

    def _transform(self, data: List[Dict]) -> Dict[str, Any]:
        """Internal transformation logic."""
        ...
```

---

## Error Handling

```python
# Specific exceptions
try:
    result = parse_config(path)
except FileNotFoundError:
    logger.error(f"Config file not found: {path}")
    raise
except json.JSONDecodeError as e:
    logger.error(f"Invalid JSON in config: {e}")
    raise ConfigurationError(f"Invalid config format: {e}")

# Context managers for cleanup
with open(path, 'r') as f:
    data = f.read()

# Custom exceptions
class ProcessingError(Exception):
    """Raised when data processing fails."""
    pass
```

---

## Context Managers

```python
from contextlib import contextmanager

@contextmanager
def database_connection(connection_string: str):
    """Manage database connection lifecycle."""
    conn = create_connection(connection_string)
    try:
        yield conn
    finally:
        conn.close()

# Usage
with database_connection(conn_str) as conn:
    results = conn.execute(query)
```

---

## List/Dict Comprehensions

```python
# Good - readable comprehension
names = [user.name for user in users if user.active]

# Bad - too complex, use regular loop
result = {
    k: [x.value for x in v if x.valid]
    for k, v in data.items()
    if v and any(x.valid for x in v)
}

# Better - break it down
result = {}
for key, values in data.items():
    if not values:
        continue
    valid_values = [x.value for x in values if x.valid]
    if valid_values:
        result[key] = valid_values
```

---

## Virtual Environments

Always use virtual environments:

```bash
# Create
python -m venv venv

# Activate (Windows)
.\venv\Scripts\Activate.ps1

# Activate (Linux/Mac)
source venv/bin/activate

# Requirements
pip freeze > requirements.txt
pip install -r requirements.txt
```

---

## Common Pitfalls

```python
# ❌ Mutable default argument
def add_item(item, items=[]):
    items.append(item)
    return items

# ✅ Use None instead
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items

# ❌ Bare except
try:
    risky_operation()
except:
    pass

# ✅ Specific exception
try:
    risky_operation()
except SpecificError as e:
    logger.error(f"Operation failed: {e}")
    raise
```
