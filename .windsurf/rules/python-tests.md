---
trigger: glob
globs: ["**/test_*.py", "**/*_test.py", "**/tests/**/*.py"]
description: Python testing standards - automatically loaded when working with test files
---

# Python Testing Standards

## Framework

- Python: pytest with pytest-cov, pytest-mock
- Async: pytest-asyncio

---

## Directory Structure

```
tests/
├── unit/              # Fast, isolated tests
│   ├── {module}/      # Mirror src/ structure
│   └── conftest.py    # Shared fixtures
├── integration/       # Tests with real dependencies
│   └── conftest.py
└── e2e/               # End-to-end (if applicable)
```

---

## File Placement

| Type | Location |
|------|----------|
| Unit tests | `tests/unit/{module}/test_*.py` |
| Integration tests | `tests/integration/test_*.py` |
| Test utilities | `tests/utilities/` |
| Test fixtures | `tests/fixtures/` |

**NEVER** create test files in project root.

---

## Naming Conventions

- **Files:** `test_{module_name}.py`
- **Functions:** `test_{function_name}_{scenario}`
- **Classes:** `Test{ClassName}`

---

## Test Structure (Arrange-Act-Assert)

```python
def test_creates_valid_token(mock_user):
    # Arrange - set up test data
    user = User(id=1, name="Test")

    # Act - perform the action
    token = create_token(user)

    # Assert - verify results
    assert token is not None
    assert len(token) > 0
```

---

## Best Practices

- Use fixtures for setup/teardown
- Use `pytest.mark.parametrize` for multiple inputs
- Mock external services - never call real APIs in unit tests
- Integration tests can use test database
- Test behavior, not implementation

---

## Coverage Requirements

| Type | Target |
|------|--------|
| Minimum | 80% line coverage |
| Critical paths | 100% branch coverage |
| Error handling | 100% |

---

## Example

```python
# tests/unit/auth/test_jwt_handler.py
import pytest
from src.auth.jwt_handler import create_token, validate_token

class TestCreateToken:
    def test_creates_valid_token(self, mock_user):
        token = create_token(mock_user)
        assert token is not None

    def test_raises_on_invalid_user(self):
        with pytest.raises(ValueError):
            create_token(None)
```

---

## Before Declaring Complete

- [ ] Unit tests written and passing
- [ ] Run `pytest tests/unit/ -v`
- [ ] Run actual execution (not just tests)
- [ ] Check logs for warnings/errors
