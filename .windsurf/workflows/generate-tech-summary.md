---
name: generate-tech-summary
description: Generate or update tech summary documentation for modules. Usage: /generate-tech-summary
auto_execution_mode: 0
---

# Generate Tech Summary

Create or update technical summary documentation for modules.

**Purpose:** Fresh sessions load summaries (~2KB) instead of full source (~50KB).

---

## Step 1: Identify Scope

Ask or determine:

| Question | Answer |
|----------|--------|
| Which layer? | {backend/api/frontend/etc} |
| Which module(s)? | {specific module or "all modified"} |
| Full regenerate or update? | {new/update} |

**If invoked from /phase-complete:** Use modules created/modified in the completed phase.

---

## Step 2: Locate Source Files

For each module to document:

```bash
ls -la src/{layer}/{module}/
```

Identify:
- Main classes/files
- Public interfaces
- Entry points

---

## Step 3: Analyze & Generate

For each module, read source files and extract:

### Public API
- Class names and purpose (one-liner)
- Constructor signatures with types
- Public method signatures with return types
- Standalone functions if any

### Dependencies
- **Uses:** What this module imports from project
- **Used By:** What imports this module (grep for imports)
- **External:** Third-party libraries used

### Patterns
- Design patterns used (Factory, Repository, Strategy, etc.)
- Architecture patterns (if notable)

### Config & Testing
- Environment variables or config keys
- Test file location
- Key fixtures or mocking notes

---

## Step 4: Write Summary File

Create/update: `docs/tech-summaries/{layer}/{module}.md`

**Template:**

```markdown
# {Module Name}

**Last Updated:** {YYYY-MM-DD}
**Location:** `src/{layer}/{module}/`

---

## Overview

{1-2 sentences: What this module does}

---

## Public API

### {ClassName}

**Purpose:** {One-liner}

**Constructor:**
```{language}
def __init__(self, {params}: {types}) -> None:
```

**Key Methods:**
```{language}
def method_name(self, {params}) -> {ReturnType}:
    """Brief description."""
```

---

## Dependencies

**Uses (project imports):**
- `{module.Class}` - {why}

**Used By:**
- `{other_module}` - {context}

**External:**
- `{library}` - {purpose}

---

## Design Patterns

- {Pattern}: {one-line explanation}

---

## Configuration

- `{CONFIG_KEY}`: {purpose} (default: {value})

---

## Testing

- **Test file:** `tests/unit/{layer}/test_{module}.py`
- **Fixtures:** {key fixtures}
- **Mocking:** {what to mock}
```

---

## Step 5: Update Index (if needed)

If new module, add to `docs/tech-summaries/{layer}/_index.md`:

```markdown
## {Layer} Modules

| Module | Purpose | Location |
|--------|---------|----------|
| {module} | {one-liner} | `src/{layer}/{module}/` |
```

Create `_index.md` if it doesn't exist.

---

## Step 6: Verify

- [ ] All public classes documented
- [ ] All public methods have signatures
- [ ] Dependencies are accurate (check imports)
- [ ] File saved to correct location

---

## Output

```
✅ TECH SUMMARY GENERATED

File: docs/tech-summaries/{layer}/{module}.md
Classes: {N}
Methods: {N}
Dependencies: {N} internal, {N} external

{If index updated:}
Index updated: docs/tech-summaries/{layer}/_index.md
```

---

## Quick Reference

| Scenario | Action |
|----------|--------|
| Single module | `/generate-tech-summary` → specify module |
| After phase complete | Automatic via `/phase-complete` |
| Entire layer | `/generate-tech-summary` → specify layer, "all" |
| Quick update | Edit existing file directly |
| Check freshness | Ask for validation mode |

---

## Validation Mode (Optional)

**When to use:** Check if summaries match source without regenerating.

Ask: *"Can you validate the tech summaries first?"* or *"Just check if summaries are current"*

### Process

```
1. Load existing summary: docs/tech-summaries/{layer}/{module}.md
2. Read current source: src/{layer}/{module}/
3. Compare:
   - Public classes/functions
   - Method signatures
   - Dependencies
4. Report mismatches
```

### Output

```
🔍 VALIDATION: {module}

Status: {✅ Current | ⚠️ Stale | ❌ Missing}

{If stale:}
Mismatches found:
- Method `process()` signature changed
- New class `Helper` not in summary
- Dependency `utils` removed

Options:
[R] Regenerate summary now
[I] Ignore and continue
```

### Automatic Validation

`/plan-task` automatically validates summaries for modules it loads.

---

## Examples

**Single module:**
```
/generate-tech-summary
Layer: ui_layer
Module: parsers
```

**Multiple modules after phase:**
```
/generate-tech-summary
Layer: ui_layer
Modules: parsers, enrichers (modified in Phase 3)
```