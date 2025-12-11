---
trigger: glob
globs: ["**/*.py"]
---

# Python Standards

## File Limits

- **Max 650 lines** per file (split if larger)
- **Max 50 lines** per method (refactor if larger)

## File Placement

**Tests:**
- Unit tests → `tests/unit/{layer}/test_*.py` where layer is:
  - `sql_layer/` - SQL layer unit tests
  - `model_layer/` - Model layer unit tests
  - `ui_layer/` - UI layer unit tests
  - `integration_layer/` - Integration layer unit tests
  - `common/` - Common utilities unit tests
- Integration tests → `tests/integration/{layer}/test_*.py` (organized by layer)
- Test utilities → `tests/utilities/`
- Test data/fixtures → `tests/fixtures/`
- Research/experimental → `tests/research/`
- Archived tests → `tests/archive/`

**Scripts:** → `scripts/`

**Source code:**
- SQL Layer → `src/sql_layer/`
- Model Layer → `src/model_layer/`
- UI Layer → `src/ui_layer/`
- Shared → `src/common/`

**NEVER create .py files in project root** (except `main.py`)

## Required in Every File

```python
# Logging
from common.logger import setup_logger
logger = setup_logger(__name__)

# Type hints on public methods
def process(self, data: List[Dict]) -> Dict[str, Any]:

# Docstrings (Google style)
"""Brief description.

Args:
    data: Input data description
    
Returns:
    Output description
"""

# Error handling
try:
    result = self._do_work()
except SpecificError as e:
    self.logger.error(f"Failed: {e}", exc_info=True)
    raise
```

## Testing Requirements

**Before declaring task complete:**
- [ ] Unit tests written and passing
- [ ] Run `pytest tests/unit/ -v`
- [ ] **Run actual execution** (not just tests)
- [ ] Check logs and terminal output for warnings/errors

## Common Utilities

```python
from common.config_loader import ConfigLoader
from common.ai_service import AIServiceFactory
from common.logger import setup_logger
```

**Never hardcode** - use `config/config.yaml`