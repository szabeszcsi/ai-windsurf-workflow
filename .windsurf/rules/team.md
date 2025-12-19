---
trigger: model
description: Team configuration - developer to context file mapping
---

# Team Configuration

At session start:
- Ask who the developer is
- Load the mapped `dev{ID}_context.md`

---

## Developers

| ID | Name | Context File | Domain |
|----|------|--------------|--------|
| 1 | Ferran | dev1_context.md | SQL Layer |
| 2 | Szabi | dev2_context.md | Model/UI/Integration |

---

## Usage

Single-developer projects: Use `dev_context.md` directly.
Multi-developer projects: Reference this file for context mapping.
