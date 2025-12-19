---
trigger: manual
description: Deep reference for framework tuning and rare checklists. Activate via @framework-reference
---
# Framework Reference

## When to use
- Tuning the AI meta-framework (rules/workflows)
- Unclear system behavior / enforcement
- Needing deep checklists (planning, verification, testing, summaries)

## Where guidance should live (efficiency)
- **Always-on rules:** only hard rails (safety, placement, transparency)
- **Glob rules:** enforcement that must be visible while editing files
- **Workflows:** procedures + sequencing (tests → docs → context → git)
- **Manual rules:** deep reference / rarely-needed detail
- **Model-decision rules:** optional situational guards (best-effort)

## Tech summaries (honest)
- Summaries help only if they are **actually loaded into context**.
- Prefer reading `docs/tech-summaries/...` before reading large source files.
- Validate freshness quickly (spot-check source exports/signatures) before trusting.

## Python discipline
- Editing source (`src/**/*.py`): ensure `python-master` is active (includes a test gate).
- Before declaring complete: run the relevant `pytest` scope.

## Phase completion discipline
- If a phase is “done”: switch to `/phase-complete` and treat it as blocking.
- After completion: start the next phase in a new chat via `/start-session`.
