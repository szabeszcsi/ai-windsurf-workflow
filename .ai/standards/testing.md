# Testing Standards

## Framework
- Python: pytest with pytest-cov, pytest-mock
- Async: pytest-asyncio

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

## Naming Conventions
- Files: `test_{module_name}.py`
- Functions: `test_{function_name}_{scenario}`
- Classes: `Test{ClassName}`

## Patterns
- Use fixtures for setup/teardown
- Use `pytest.mark.parametrize` for multiple inputs
- Mock external services, never call real APIs in unit tests
- Integration tests can use test database

## Coverage Requirements
- Minimum: 80% line coverage
- Critical paths: 100% branch coverage

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