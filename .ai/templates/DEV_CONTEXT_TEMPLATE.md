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
# Developer {N} - {Name} ({Domain})

<!-- AI: Archive when >1.5KB -->

**Name:** {Name}
**Focus:** {Feature Name} Phase {N}
**Updated:** {Date Time}

---

## 🌿 Branch
**Current:** `feature/{feature-name}`
**Status:** {Clean / Uncommitted changes / Ready to push}

---

## 🎯 Primary Task
**{Feature Name}** - Phase {N} 🚧
- Status: {X}% ({N}/{N} subtasks complete)
- Next: {Next immediate step}
- Handoff: `docs/tasks/{feature}_phase{N}_handoff.md`

---

## 🔒 Task Constants (DO NOT MODIFY)
**Task:** {Feature Name} (Phases 1-{N})

- **Test:** `tests/integration/{test_file}.py`
- **Schema:** `src/{layer}/{component}/{file}.py` - {Notes}
- **Constructor:** `{ClassName}({param1}, {param2}, {param3})`

---

## 🔥 Lingering ({count})
1. **{Bug/Issue description}** - 🟡 ✅ {Status}
2. **{Another issue}** - 🟢 🚧 {Status}

---

## ✅ Recent (Last 3)
1. ✅ {Completion 1} ({date})
2. ✅ {Completion 2} ({date})
3. ✅ {Completion 3} ({date})

---

## 📁 References
- Task: `docs/tasks/{feature}_tasks.md`
- Archive: `docs/archive/dev{N}_sessions_{YYYY-MM}.md`

---

## 🚀 Next Session
\```
I'm {Name}. {Feature} Phase {N} - {brief status}.
Branch: feature/{feature-name}
{N} items remaining.
\```
```

This is ~1.4 KB - still within safe limits.
