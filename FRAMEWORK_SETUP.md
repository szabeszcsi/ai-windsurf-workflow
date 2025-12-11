# Windsurf AI Framework - Setup Guide

**Multi-developer AI workflow framework optimized for Windsurf IDE + Claude**

This framework manages context, coding standards, and task handoffs for AI-assisted development across multiple developers and sessions.

---

## What Is This Framework?

A portable, production-ready system for:
- ✅ Managing AI context across multiple chat sessions
- ✅ Coordinating work between multiple developers
- ✅ Maintaining coding standards automatically
- ✅ Tracking task progress through phases
- ✅ Preserving critical decisions (Task Constants)
- ✅ Optimizing token usage (40%+ savings)

**Key Features:**
- **Context preservation** - Never lose track of work between sessions
- **Multi-developer support** - Each dev has isolated context
- **Auto-triggered rules** - Coding standards load based on file type
- **Workflow automation** - Guided workflows for common tasks
- **Token-optimized** - Two-tier documentation system saves tokens

---

## Prerequisites

Before installing this framework, ensure you have:

- ✅ **Windsurf IDE** installed
- ✅ **Git repository** initialized in your project
- ✅ **Project language** - Currently supports Python (extensible to others)
- ✅ **Basic familiarity** with AI-assisted development

---

## Quick Install (5 Minutes)

### 1. Copy Framework Files

Copy these folders to your project root:

```bash
# Copy the framework structure
cp -r .windsurf/ /your/project/
cp -r .ai/ /your/project/
```

Your project should now have:
```
your-project/
├── .windsurf/           # Windsurf-specific rules and workflows
│   ├── rules/
│   └── workflows/
├── .ai/                 # AI framework documentation and templates
│   ├── standards/
│   └── templates/
```

### 2. Create Developer Context File

Create `dev_context.md` in your project root:

```bash
# For single-developer projects
cp .ai/templates/DEV_CONTEXT_TEMPLATE.md dev_context.md

# Edit dev_context.md and fill in:
# - Your name
# - Current branch
# - Active tasks
```

### 3. Test the Installation

Open Windsurf and start a new chat:

```
/start-session
```

If the AI:
- ✅ Loads your dev_context.md
- ✅ Asks what you want to work on
- ✅ Shows available workflows

**Success!** The framework is installed.

---

## Detailed Setup

### Step 1: Copy Framework Files

Copy the complete framework structure:

```
.windsurf/
├── rules/
│   ├── core-rules.md          # Always-on core behaviors
│   ├── team.md                # Multi-developer configuration
│   ├── python-code.md         # Python coding standards (auto-triggered)
│   └── python-tests.md        # Python testing standards (auto-triggered)
└── workflows/
    ├── start-session.md       # Session initialization
    ├── update-context.md      # Save progress mid-session
    ├── phase-complete.md      # Phase completion protocol
    ├── check-status.md        # Context health check
    ├── reload-context.md      # Emergency recovery
    ├── abort.md               # Emergency rollback
    ├── plan-task.md           # Task planning
    ├── generate-architecture.md
    └── generate-tech-summary.md

.ai/
├── AGENT_REFERENCE.md         # AI agent system reference
├── standards/
│   ├── python.md              # Full Python coding standards
│   └── testing.md             # Full testing standards
└── templates/
    ├── HANDOFF_TEMPLATE.md
    ├── TASK_FILE_TEMPLATE.md
    └── SOLUTION_ARCHITECTURE_TEMPLATE.md
```

### Step 2: Configure for Your Team

#### Single Developer (Simple)

Create `dev_context.md` in project root:

```markdown
# Developer Context

**Developer:** Your Name
**Branch:** `main` or `feature/your-feature`

---

## 🎯 Primary Task
None - Ready to start

---

## 🔥 Lingering Tasks
None

---

## ✅ Recent Completions
None

---

## 🔒 Task Constants
None yet - Will be added as work progresses
```

#### Multiple Developers (Team)

**A) Keep `.windsurf/team.md` and configure it:**

Edit `.windsurf/team.md`:

```markdown
# Team Configuration

## Developers

| ID | Name | Context File | Primary Domain |
|----|------|--------------|----------------|
| 1  | Alice | dev1_context.md | Backend/API |
| 2  | Bob   | dev2_context.md | Frontend/UI |
| 3  | Carol | dev3_context.md | Database/SQL |
```

**B) Create context files for each developer:**

```bash
# Create individual dev context files
cp dev_context.md dev1_context.md
cp dev_context.md dev2_context.md
cp dev_context.md dev3_context.md

# Edit each file with developer-specific info
```

**C) Each developer starts sessions with:**

```
/start-session
# AI will ask: "WHO ARE YOU?"
# Developer answers: "Alice" (or "1")
# AI loads dev1_context.md
```

### Step 3: Create Project Documentation

#### Optional but Recommended

Create `SOLUTION_ARCHITECTURE.md`:

```bash
# Use the workflow to generate it
/generate-architecture
```

Or use the template:
```bash
cp .ai/templates/SOLUTION_ARCHITECTURE_TEMPLATE.md SOLUTION_ARCHITECTURE.md
# Edit to match your project
```

Create `PROJECT_STATUS.md`:

```markdown
# Project Status

**Project:** Your Project Name
**Status:** In Development
**Current Phase:** Phase 1 - Setup

## Active Work
- Setting up AI framework
- Initial project structure

## Recent Changes
- {date}: Framework installed
```

### Step 4: Initialize Directory Structure

Create the directories the framework expects:

```bash
mkdir -p docs/tasks
mkdir -p docs/tasks/completed
mkdir -p docs/working
mkdir -p docs/archive
mkdir -p docs/tech-summaries
```

### Step 5: Configure Git

Update `.gitignore` to exclude sensitive files:

```bash
# Add to .gitignore
dev_context.md
dev1_context.md
dev2_context.md
dev3_context.md
docs/working/
*.bak

# Keep framework files
!.windsurf/
!.ai/
```

### Step 6: Test the Setup

Start Windsurf and test each workflow:

```bash
# 1. Test session start
/start-session

# 2. Test status check
/check-status

# 3. Test context update (make a small change first)
/update-context

# 4. Test context reload
/reload-context
```

If all workflows execute without errors, you're set up correctly!

---

## Customization Guide

### Adding New Language Support

Example: Adding JavaScript support

**1. Create full standard:**

Create `.ai/standards/javascript.md`:

```markdown
# JavaScript Coding Standards

## Required in Every File
- ESLint configuration
- Proper imports/exports
- JSDoc comments

## Naming Conventions
- Files: kebab-case
- Classes: PascalCase
- Functions: camelCase
- Constants: UPPER_SNAKE

[... full JavaScript standards ...]
```

**2. Create condensed rule:**

Create `.windsurf/rules/javascript-code.md`:

```markdown
---
trigger: glob
globs: ["**/*.js", "**/*.jsx", "!**/*.test.js", "!**/*.spec.js"]
description: JavaScript coding standards
---

# JavaScript Code Standards

**Full reference:** `.ai/standards/javascript.md`

## File Limits
| Metric | Limit |
|--------|-------|
| Lines per file | 500 max |
| Lines per function | 50 max |

## Quick Patterns
- Use ESLint
- Modern ES6+ syntax
- Async/await over promises
- JSDoc on public functions

[... condensed patterns ...]
```

**3. Update core-rules:**

Add to `.windsurf/rules/core-rules.md` "Load On Demand" table:

```markdown
| Writing JavaScript | `.ai/standards/javascript.md` |
```

**4. Test:**

Open a `.js` file in Windsurf - the AI should auto-load `javascript-code.md`.

### Modifying Python Standards

Edit both files to keep them in sync:

1. **Edit `.ai/standards/python.md`** - Make your changes
2. **Edit `.windsurf/rules/python-code.md`** - Update summary if needed
3. **Keep the reference:** Ensure rule file still has `**Full reference:** .ai/standards/python.md`

### Creating Custom Workflows

Create `.windsurf/workflows/your-workflow.md`:

```markdown
---
name: your-workflow
description: What this workflow does
auto_execution_mode: 0
---

# Your Workflow Name

## Step 1: First Step
Instructions...

## Step 2: Second Step
Instructions...
```

Then invoke with: `/your-workflow`

---

## Troubleshooting

### AI Not Loading Rules

**Symptom:** Python file open, but AI doesn't follow Python standards

**Solutions:**
1. Check `.windsurf/rules/python-code.md` has correct trigger:
   ```yaml
   trigger: glob
   globs: ["**/*.py", ...]
   ```
2. Restart Windsurf IDE
3. Verify file is in project workspace (not external)

### Workflows Not Found

**Symptom:** `/start-session` says "command not found"

**Solutions:**
1. Verify `.windsurf/workflows/` exists
2. Check workflow file has frontmatter:
   ```yaml
   ---
   name: start-session
   ---
   ```
3. Restart Windsurf

### Context Files Not Found

**Symptom:** `/start-session` can't find `dev_context.md`

**Solutions:**
1. Verify `dev_context.md` exists in project root
2. Check file permissions (readable)
3. For multi-dev: Check `.windsurf/team.md` mapping

### AI Seems Confused

**Symptom:** AI re-reads files, asks answered questions

**Solutions:**
1. Run `/check-status` - AI will self-diagnose
2. Run `/reload-context` - Emergency recovery
3. Start new chat with `/start-session`
4. Check context file size (should be < 2KB)

---

## Understanding the System

### Two-Tier Documentation

The framework uses a **two-tier system** to save tokens:

**Tier 1: Auto-triggered rules** (`.windsurf/rules/`)
- Condensed summaries (~150 lines)
- Loaded automatically when editing matching files
- Example: Edit `.py` file → Loads `python-code.md`

**Tier 2: Full standards** (`.ai/standards/`)
- Complete reference (~250+ lines)
- Loaded on-demand when needed
- Example: AI needs details → Reads `python.md`

**Result:** 40%+ token savings while maintaining full documentation access

### Workflow System

Workflows guide AI through common tasks:

- `/start-session` - Begin new chat session
- `/update-context` - Save progress mid-session
- `/phase-complete` - Complete a phase, create handoff
- `/check-status` - Health check and status report
- `/reload-context` - Emergency context recovery
- `/abort` - Emergency rollback

### Task Constants

Critical decisions that must be preserved across sessions:

```markdown
## 🔒 Task Constants

| Item | Value | Established | Notes |
|------|-------|-------------|-------|
| Test script | `scripts/test_setup.sh` | Phase 1 | DO NOT RECREATE |
| Constructor | `Parser(config, logger)` | Phase 2 | DO NOT CHANGE SIGNATURE |
```

These prevent AI from breaking working code in later sessions.

---

## Next Steps

After installation:

1. **Read:** `.ai/AGENT_REFERENCE.md` (optional - for understanding architecture)
2. **Learn workflows:** Try each `/workflow` command
3. **Start first task:** Use `/plan-task` to create structured work
4. **Iterate:** Use `/update-context` to save progress regularly

---

## Getting Help

- **Framework issues:** Check `.ai/AGENT_REFERENCE.md`
- **Workflow questions:** Read workflow files in `.windsurf/workflows/`
- **AI confusion:** Run `/check-status` or `/reload-context`
- **Emergency:** Run `/abort` to rollback changes

---

## Framework Philosophy

1. **Explicit over implicit** - Clear files, clear names
2. **Lazy loading** - Load what's needed, when needed
3. **Context preservation** - Never lose work between sessions
4. **Token efficiency** - Optimize for cost and speed
5. **Multi-developer ready** - Scale to teams easily

---

*Framework Version: 2.0*
*Last Updated: 2025-12-11*
