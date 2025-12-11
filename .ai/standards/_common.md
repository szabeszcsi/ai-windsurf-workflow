# Common Coding Standards

Universal principles that apply to all languages.

---

## File Limits

| Metric | Limit |
|--------|-------|
| Lines per file | 500-650 max |
| Lines per function/method | 50 max |
| Nesting depth | 4 levels max |

**If a file exceeds limits:** Split into logical modules.

---

## Error Handling

```
DO:
✅ Catch specific exceptions
✅ Log errors with context
✅ Fail fast on unrecoverable errors
✅ Provide meaningful error messages

DON'T:
❌ Catch generic Exception (unless re-raising)
❌ Silently swallow errors
❌ Return null/None to indicate error (use exceptions)
```

---

## Comments & Documentation

### When to Comment
- **Why**, not **what** - code shows what, comments explain why
- Complex algorithms
- Non-obvious business logic
- Workarounds and TODOs

### When NOT to Comment
- Obvious code (`i += 1  # increment i`)
- Code that should be refactored to be clearer

### Format
```
# Single line for brief notes

# Multi-line for longer explanations
# that need more context to understand
# the reasoning behind the code.
```

---

## Magic Numbers & Strings

```
DON'T:
❌ if status == 3:
❌ timeout = 30000

DO:
✅ STATUS_COMPLETE = 3
✅ if status == STATUS_COMPLETE:
✅ TIMEOUT_MS = 30000
```

Define constants at module/class level with descriptive names.

---

## Testing Structure

### Arrange-Act-Assert Pattern
```
# Arrange - set up test data and conditions
# Act - perform the action being tested
# Assert - verify the results
```

### Test Naming
- Describe what is being tested
- Describe the scenario
- Describe expected outcome

Example: `test_parse_report_with_empty_pages_returns_empty_list`

---

## Coverage Targets

| Type | Target |
|------|--------|
| New code | 80%+ |
| Critical paths | 100% |
| Error handling | 100% |
| Edge cases | As many as practical |

---

## Git Commits

### Message Format
```
type(scope): Brief description

Longer explanation if needed.

- Detail 1
- Detail 2
```

### Types
- `feat` - New feature
- `fix` - Bug fix
- `refactor` - Code change that neither fixes nor adds
- `test` - Adding/updating tests
- `docs` - Documentation only
- `chore` - Maintenance tasks

### Rules
- Commit working code
- One logical change per commit
- Write meaningful messages
- Don't commit commented-out code

---

## Code Review Checklist

Before considering code complete:

- [ ] Follows language-specific standards
- [ ] Error handling is appropriate
- [ ] No hardcoded magic values
- [ ] Functions/methods are focused (single responsibility)
- [ ] Names are descriptive
- [ ] Tests exist and pass
- [ ] No debug/temporary code left behind
