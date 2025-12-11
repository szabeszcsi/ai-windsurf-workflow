---
trigger: glob
globs: ["**/test_*.py", "**/*_test.py", "**/tests/**/*.py"]
description: Python testing standards
---

# Python Testing Standards

**Full reference:** `.ai/standards/testing.md`

---

## File Placement

| Test Type | Location | Naming |
|-----------|----------|--------|
| Unit tests | `tests/unit/{module}/` | `test_{module}.py` |
| Integration | `tests/integration/` | `test_{feature}.py` |
| Fixtures | `tests/fixtures/` | descriptive names |
| Utilities | `tests/utilities/` | `{helper}.py` |

**Mirror source structure:** `src/auth/handler.py` → `tests/unit/auth/test_handler.py`

---

## Test Structure (AAA Pattern)

```python
def test_creates_valid_token_for_active_user():
    # Arrange
    user = User(id=1, name="Test", active=True)
    
    # Act
    token = create_token(user)
    
    # Assert
    assert token is not None
    assert len(token) > 0
```

---

## Naming Convention

Pattern: `test_{what}_{condition}_{expected}`

```python
# ✅ Good - descriptive
def test_parse_config_with_missing_file_raises_error():
def test_calculate_total_with_empty_list_returns_zero():

# ❌ Bad - vague
def test_parse():
def test_it_works():
```

---

## Key Practices

- Use `pytest` fixtures for setup/teardown
- Use `pytest.mark.parametrize` for multiple inputs
- Mock external services - never call real APIs in unit tests
- Test behavior, not implementation details

---

## Coverage

| Type | Target |
|------|--------|
| New code | 80% minimum |
| Critical paths | 100% |
| Error handling | 100% |

---

## What to Test

| Category | Examples |
|----------|----------|
| Happy path | Valid inputs, expected flow |
| Edge cases | Empty, boundaries, None, large inputs |
| Error cases | Invalid inputs, failures, timeouts |

---

## Before Complete

- [ ] `pytest tests/unit/{module}/ -v` passes
- [ ] No hardcoded test values (use fixtures/constants)
- [ ] Mocks used for external dependencies