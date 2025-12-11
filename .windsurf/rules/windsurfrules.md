---
trigger: manual
description: Quick reference card. Load with /help or when needed.
---

# Quick Reference Card

## Commands

| Command | When | Priority |
|---------|------|----------|
| `/start-session` | Every new chat | 🔴 Required |
| `/phase-complete` | Phase done, before commit | 🔴 Required |
| `/check-status` | Verify context health | 🟡 Periodic |
| `/update-context` | Mid-phase progress save | 🟢 Optional |
| `/reload-context` | Lost/confused | 🟡 Recovery |
| `/abort` | Emergency rollback | 🔴 Emergency |

## File Locations

```
tests/unit/          → Unit tests
tests/integration/   → Integration tests  
tests/utilities/     → Test helpers
scripts/             → Utility scripts
src/{layer}/         → Source code
docs/tasks/          → Handoffs & completions
docs/working/        → Temp files
docs/archive/        → Old sessions
```

## ⛔ Never

- Assume developer identity
- Commit without `/phase-complete`
- Continue chat after phase complete
- Create files in project root
- Write implementation code in chat
- Ignore 🚨 prompts

## Context Health

| Size | Status |
|------|--------|
| < 1.5 KB | ✅ Healthy |
| 1.5-2 KB | ⚠️ Archive soon |
| > 2 KB | 🚨 Archive now |

## Developers

- **Ferran** → `dev1_context.md` → SQL Layer
- **Szabi** → `dev2_context.md` → Model/UI/Integration
