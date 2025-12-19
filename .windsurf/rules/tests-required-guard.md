---
trigger: model
description: Require unit tests when Python source behavior changes (model-decision fallback)
---

# Tests Required Guard

**Apply when user asks to:**
- Add a feature
- Change behavior
- Refactor logic
- Fix a bug

**AND** work touches Python under `src/`.

---

## Required Behavior

Before finishing:
1. Ensure unit tests added/updated under `tests/unit/` (mirrored structure)
2. Run relevant pytest scope
3. Verify tests pass

---

## Minimal Test Expectations

- Happy path
- Edge case
- Error case (where applicable)

---

## Waiver Protocol

If user explicitly waives tests → record that decision in response.

---

## Prohibited

- Do not change working code just to satisfy tests
- Do not call real external services in unit tests (mock them)
