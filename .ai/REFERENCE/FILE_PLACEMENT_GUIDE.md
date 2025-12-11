# File Placement Guide

**Quick reference for where to put different types of files.**

**Last Updated:** November 26, 2025

---

## 📁 Directory Structure

```
PowerBI-Documentation-Suite/
├── docs/
│   ├── tasks/                          # ✅ Task files and phase handoffs
│   │   ├── {layer}_tasks.md            # Main task file
│   │   ├── {layer}_phase{N}_handoff.md # Active phase handoffs
│   │   └── completed/                  # Completed phase handoffs
│   │
│   ├── ai/                             # ✅ AI meta-documentation
│   │   ├── TASK_FILE_GENERATION_GUIDE.md  # How to create task files
│   │   ├── TEMPLATES/                  # Copy-paste templates
│   │   ├── REFERENCE/                  # Examples and guides
│   │   └── archive/                    # Historical documents
│   │
│   ├── {LAYER}_ARCHITECTURE.md         # ✅ Architecture documents
│   └── archive/                        # ✅ Archived documents
│
├── scripts/                            # ✅ Utility scripts
│
├── .github/
│   └── copilot-instructions.md         # ✅ Coding standards
│
├── .windsurf/rules/
│   └── windsurfrules.md                # ✅ Windsurf workflow rules
│
├── PROJECT_STATUS.md                   # ✅ Project-wide status
├── dev1_context.md                     # ✅ Ferran's context
└── dev2_context.md                     # ✅ Szabi's context
```

---

## 📋 File Type → Location Map

### Task Files
**Location:** `docs/tasks/`  
**Naming:** `{layer}_tasks.md`  
**Examples:**
- `integration_layer_tasks.md`
- `ui_layer_tasks.md`
- `sql_layer_refactoring_tasks.md`

### Phase Handoffs (Active)
**Location:** `docs/tasks/`  
**Naming:** `{layer}_phase{N}_handoff.md`  
**Examples:**
- `integration_layer_phase1_handoff.md`
- `ui_layer_phase3_handoff.md`

### Phase Handoffs (Completed)
**Location:** `docs/tasks/completed/`  
**Naming:** `{layer}_phase{N}_handoff.md`  
**Action:** Move here when phase is complete

### Architecture Documents
**Location:** `docs/`  
**Naming:** `{LAYER}_ARCHITECTURE.md`  
**Examples:**
- `INTEGRATION_LAYER_ARCHITECTURE.md`
- `UI_LAYER_ARCHITECTURE.md`

### AI Meta-Documentation
**Location:** `docs/ai/`  
**Purpose:** How to use AI tools, create task files, etc.  
**Key Files:**
- `TASK_FILE_GENERATION_GUIDE.md` - Main guide for task creation
- `TEMPLATES/` - Copy-paste templates
- `REFERENCE/` - Examples and guides

### Utility Scripts
**Location:** `scripts/`
**Purpose:** Automation, setup, cleanup
**Examples:**
- `clean_pycache.ps1`
- `setup_git_hooks.ps1`

### Tech Summaries (Multi-Session Continuity)
**Location:** `docs/tech-summaries/{layer}/{module}.md`
**Purpose:** Fast architecture understanding for fresh sessions
**Structure:**
- `_index.md` - 1-page project overview
- `{layer}/` - Per-layer summaries (backend/, api/, frontend/)

**When:** Update after each code modification in multi-layer projects
**Template:** `.ai/templates/TECH_SUMMARY_TEMPLATE.md`

**Benefits:**
- Fresh sessions: Read summaries (2KB) vs full source (50KB)
- Architecture awareness without file exploration
- 10x faster context loading

---

## ✅ Quick Decision Tree

**I'm creating a...**

### Task File
→ `docs/tasks/{layer}_tasks.md`

### Phase Handoff (new phase starting)
→ `docs/tasks/{layer}_phase{N}_handoff.md`

### Phase Handoff (phase complete)
→ Move to `docs/tasks/completed/{layer}_phase{N}_handoff.md`

### Architecture Document
→ `docs/{LAYER}_ARCHITECTURE.md`

### Troubleshooting Guide
→ `docs/ai/{ISSUE}_TROUBLESHOOTING.md`

### AI Workflow Guide
→ `docs/ai/{TOPIC}_GUIDE.md`

### Utility Script
→ `scripts/{purpose}.ps1` or `.sh`

### Developer Onboarding
→ `docs/ONBOARDING.md`

### Tech Summary (for module/class)
→ `docs/tech-summaries/{layer}/{module}.md`

---

## 🚫 Common Mistakes

### ❌ Wrong
```
docs/ai/PHASE_1_HANDOFF.md
docs/ai/integration_layer_phase1_handoff.md
docs/PHASE_1_HANDOFF.md
```

### ✅ Correct
```
docs/tasks/integration_layer_phase1_handoff.md
```

---

### ❌ Wrong
```
docs/tasks/PYADOMD_ENVIRONMENT_ISSUE.md
docs/PIPELINE_ISSUES.md
```

### ✅ Correct
```
docs/ai/PYADOMD_ENVIRONMENT_ISSUE.md
docs/ai/PIPELINE_EXECUTION_ISSUES_FIX.md
```

---

### ❌ Wrong
```
scripts/integration_layer_tasks.md
docs/clean_pycache.ps1
```

### ✅ Correct
```
docs/tasks/integration_layer_tasks.md
scripts/clean_pycache.ps1
```

---

## 📖 Related Documentation

- **Task File Generation:** `docs/ai/TASK_FILE_GENERATION_GUIDE.md` - How to create task files
- **Templates:** `docs/ai/TEMPLATES/` - Handoff and task templates
- **Workflow Rules:** `.windsurf/rules/windsurfrules.md` - Session and phase workflow
