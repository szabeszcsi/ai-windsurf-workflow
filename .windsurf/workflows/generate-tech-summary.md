---
name: generate-tech-summary
description: Generate or update tech summary documentation for modules. Usage: /generate-tech-summary
auto_execution_mode: 0
---

# Generate Tech Summary

**Purpose:** Summaries (~2KB) load faster than full source (~50KB), but only help if actually loaded into context.

---

## 1. Identify Scope

| Question | Answer |
|----------|--------|
| Layer | {backend/api/etc} |
| Module(s) | {specific or "all modified"} |
| Mode | {new/update} |

---

## 2. Locate Source

```bash
ls -la src/{layer}/{module}/
```

Identify main classes, public interfaces, entry points.

---

## 3. Extract (API Surface Focus)

**DO NOT read every line of implementation.** Focus on:

**Public API:**
- Class names + one-liner purpose
- Constructor signatures
- Public method signatures (with type hints)

**Dependencies:**
- Uses (project imports)
- Used by (what imports this)
- External (third-party)

**Patterns:**
- Design patterns used (if notable)

---

## 4. Write Summary

File: `docs/tech-summaries/{layer}/{module}.md`

```markdown
# {Module}

**Updated:** {date}
**Location:** `src/{layer}/{module}/`

## Overview
{1-2 sentences}

## Public API

### {ClassName}
**Purpose:** {one-liner}

**Constructor:**
```python
def __init__(self, {params}) -> None:
```

**Methods:**
```python
def method(self, {params}) -> {Type}:
```

## Dependencies
- Uses: {modules}
- Used by: {modules}
- External: {packages}

## Testing
- File: `tests/unit/{layer}/test_{module}.py`
```

---

## 5. Update Index

Add to `docs/tech-summaries/{layer}/_index.md`:

| Module | Purpose | Location |
|--------|---------|----------|
| {module} | {one-liner} | `src/{layer}/{module}/` |

---

## 6. Output

```
✅ TECH SUMMARY GENERATED

File: docs/tech-summaries/{layer}/{module}.md
Classes: {N}
Methods: {N}
```