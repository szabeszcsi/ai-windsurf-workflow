---
name: dev-context-template
description: Template for developer context files. Keep under 1.5KB!
---

# Developer Context Template

**Target size:** < 1.5 KB (HARD LIMIT: 2 KB)

---

## Template

```markdown
# Developer {X} - {Name} ({Domain})

<!-- AI: Archive when >1.5KB. Update after each task. -->

**Name:** {Name}  
**Focus:** {Current primary task}  
**Updated:** {Date Time}

---

## 🌿 Branch
**Current:** `{branch-name}`  
**Status:** {Clean / Uncommitted changes / Ready to push}

---

## 🎯 Primary Task
**{Task Name}** - Phase {N} {✅/🚧/⏸️}
- Status: {X}% complete
- Next: {immediate next step}
- Handoff: `docs/tasks/{layer}_phase{N}_handoff.md`

---

## 🔒 Task Constants (DO NOT MODIFY)
**Task:** {Task Name} (Phases 1-{N})
**Expires:** When task fully complete

- **Test script:** `{path to integration test}`
- **Key signatures:** `{Class(param1, param2)}` - DO NOT CHANGE
- **Fixtures:** `{paths}` - DO NOT RECREATE
- **Decisions:** {key architectural choices}

<!-- AI: Read this EVERY session. Do not modify these unless explicitly asked. -->
<!-- Size limit: 500 bytes. If larger, use external file (see below). -->

---

## 🔥 Lingering ({count})
1. **{Bug/Issue}** - {🔴/🟡/🟢} {✅/🚧}
   - {one-line description}
2. **{Another}** - {priority} {status}

---

## ✅ Recent (Last 3)
1. ✅ {Completion 1} ({date})
2. ✅ {Completion 2} ({date})
3. ✅ {Completion 3} ({date})

---

## 📁 References
- Task: `docs/tasks/{task}_tasks.md`
- Archive: `docs/archive/dev{X}_sessions_{month}.md`

---

## 🚀 Next Session
\```
I'm {Name}. {Brief context}.
Branch: {branch}
Primary: {task} Phase {N}
Lingering: {count} items
\```
```

---

## Size Management Rules

### What Goes IN Context File
- Current branch and status
- Primary task summary (3-5 lines max)
- **🔒 Task Constants** (test scripts, signatures, key decisions)
- Lingering task LIST (name + priority only)
- Last 3 completions (one line each)
- Key references
- Next session prompt

### What Goes ELSEWHERE
- Session details → `docs/working/{session}_{date}.md`
- Bug investigations → `docs/working/{bug}_{date}.md`
- Completed phases → `docs/tasks/{layer}_phase{N}_complete.md`
- Old sessions → `docs/archive/dev{X}_sessions_{month}.md`

### Archive Triggers
| Condition | Action |
|-----------|--------|
| Session > 2 days old | Archive to monthly file |
| Context > 1.5 KB (without constants) | Archive oldest sessions |
| Phase complete | Move details to completion doc |
| Lingering resolved | Move to Recent, delete session doc |
| **Task complete** | Archive 🔒 Constants to completion doc, remove from context |

---

## 🔒 Task Constants Rules

### Size Limit
- Task Constants section: **< 500 bytes**
- If larger: create `docs/working/{task}_constants.md` and reference it

### Overflow Example
```markdown
## 🔒 Task Constants (DO NOT MODIFY)
**Task:** Complex Feature (Phases 1-8)
**Details:** `docs/working/complex_feature_constants.md` ← LOAD THIS FILE

Summary:
- Test: `tests/integration/complex_test.py`
- 12 key signatures (see details file)
```

### Lifecycle
1. **Phase 1:** Create initial constants as key decisions are made
2. **Phase 2-N:** Add new constants, never remove
3. **Final phase:** Archive to completion doc, remove section from context

### What Belongs in Task Constants
✅ Test scripts and their expected behavior
✅ Constructor/method signatures that must not change
✅ Config structure keys
✅ Fixture file paths
✅ Key architectural decisions
✅ "DO NOT" rules (e.g., "Don't re-enrich all measures")

### What Does NOT Belong
❌ Session summaries (go in archive)
❌ Bug descriptions (go in Lingering or docs/working/)
❌ Progress updates (go in Primary Task section)
❌ Detailed code explanations (go in handoff docs)

---

## Example: Slim Context (~1.2 KB)

```markdown
# Developer 2 - Szabi (UI/Integration)

<!-- AI: Archive when >1.5KB -->

**Name:** Szabi  
**Focus:** UI Layer Refactoring Phase 4  
**Updated:** Nov 30, 2025 8:40 PM

---

## 🌿 Branch
**Current:** `feature/ui-layer-refactoring`  
**Status:** Ready to commit

---

## 🎯 Primary Task
**UI Layer Refactoring** - Phase 4 🚧
- Status: 90% (5/9 test failures fixed)
- Next: Fix remaining 4 test failures
- Handoff: `docs/tasks/ui_phase4_handoff.md`

---

## 🔒 Task Constants (DO NOT MODIFY)
**Task:** UI Layer Refactoring (Phases 1-5)

- **Test:** `tests/integration/run_page_enrichment_test.py`
- **Schema:** `src/ui_layer/models/output_schema.py` - V2 only
- **Constructor:** `ReportDocumenter(config, ai_service, model_data_path)`

---

## 🔥 Lingering (2)
1. **Excel generator dict bug** - 🟡 ✅ Fixed
2. **WeeklyVarianceSnapshot investigation** - 🟢 ✅ Solved

---

## ✅ Recent (Last 3)
1. ✅ Phase 3 - Visual Prompt Optimization (Nov 30)
2. ✅ Phase 2 - Button & Navigation (Nov 30)
3. ✅ Phase 1 - Output Schema (Nov 30)

---

## 📁 References
- Task: `docs/tasks/ui_layer_refactoring_tasks.md`
- Archive: `docs/archive/dev2_sessions_2025-11.md`

---

## 🚀 Next Session
\```
I'm Szabi. UI Layer Phase 4 - fixing test failures.
Branch: feature/ui-layer-refactoring
4 test failures remaining.
\```
```

This is ~1.4 KB - still within safe limits.
