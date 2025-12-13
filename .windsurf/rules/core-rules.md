---
trigger: always_on
---

# Core Rules

## 0. CHECKPOINT INTEGRITY

**On FIRST interaction or `/check-status`:**

| Situation | Action |
|-----------|--------|
| Direct memory of this session | ✅ Continue |
| Started from checkpoint/summary | 🚨 **DISCLOSE** → Recommend `/start-session` |
| Confused about state | 🔄 `/reload-context` |

**Never pretend to have direct memory when you don't.**

---

## 1. COMMUNICATION STYLE

**Tone:** Brief, precise, friendly, actionable.

**Chat Output Rules:**
- ✅ Focus on task execution
- ✅ Minimal commentary unless asked
- ❌ No unnecessary summaries
- ❌ No unprompted elaboration
- ❌ No "here's what I did" walls of text

**When to elaborate:**
- User explicitly asks for details
- Error requires explanation
- Workflow step requires confirmation

**Default response pattern:**
```
[Action taken]
[Result if relevant]
[Next step or question if needed]
```

---

## 2. DOCUMENT CREATION POLICY

**Create documents ONLY when:**
- ✅ Workflow explicitly requires it (e.g., `/generate-architecture`)
- ✅ User explicitly requests it
- ✅ Rule explicitly mandates it (e.g., phase handoff)
- ✅ User approves after AI proposes it

**Proactive documentation exception:**

If AI believes detailed documentation would help user understanding BEFORE taking action:
1. **Stop and propose:** "I'd like to create `docs/working/{name}.md` to clarify {reason}. Approve?"
2. **Wait for approval**
3. Only create if user says yes

**NEVER create:**
- ❌ Unrequested summaries
- ❌ "Helpful" documentation without asking first
- ❌ Status reports (unless workflow says so)
- ❌ README updates (unless asked)

**Working documents:**
- All temporary/working docs → `docs/working/`
- Only permanent docs in project root or `docs/`

---

## 3. SESSION START

Every new chat: **Run `/start-session`**

Multi-developer teams: See `.windsurf/team.md` for developer → context file mapping.

---

## 4. CONTEXT DEGRADATION

**Self-monitor for these symptoms:**
- Re-reading files already read this session
- Asking answered questions
- Creating files in wrong locations
- User says "you're confused"

**If detected:** Disclose immediately, recommend `/check-status` or new chat.

---

## 5. CODE EDITING SAFETY

- **Before multi-file edits:** Create `.bak` backups
- **After 3+ failed attempts:** Restore from backup, reassess approach

---

## 6. FILE PLACEMENT

| Type | Location |
|------|----------|
| Source code | `src/{module}/` |
| Unit tests | `tests/unit/` |
| Integration tests | `tests/integration/` |
| Test utilities | `tests/utilities/` |
| Scripts | `scripts/` |
| Task docs | `docs/tasks/` |
| Working docs | `docs/working/` |
| Archives | `docs/archive/` |

**Never in project root** except: main entry point, README, config files, dev_context.md

---

## 7. ENVIRONMENT

Before running tests, verify virtual environment:
```bash
which python  # Unix
where python  # Windows
```

---

## 8. RULE TRANSPARENCY

**Every response MUST begin with status line:**

**Format:**
- With workflow: `→ Active: {rules} | Workflow: {workflow}`
- Without workflow: `→ Active: {rules}`

**Position:** Top of response (before all content)

**Active rules include:**
- All `trigger: always_on` rules (core-rules)
- All glob-triggered rules matching current file (e.g., python-code)
- Currently executing workflow (if any)

**Examples:**

Working on Python file, no workflow:
```
→ Active: core-rules, python-code
```

Executing start-session:
```
→ Active: core-rules, python-code | Workflow: start-session
```

Working on Python test file:
```
→ Active: core-rules, python-code, python-tests
```

No files open:
```
→ Active: core-rules
```

**Purpose:**
- Verify framework working correctly
- Detect context degradation (unexpected status changes)
- Provide continuous transparency
- Enable early problem detection

**If status becomes distracting:**
- User can request: "Disable status line"
- AI will omit from subsequent responses (until re-enabled)

---

## 9. TASK ASSESSMENT

**On receiving ANY request, classify scope:**

| Scope | Criteria | AI Action |
|-------|----------|-----------|
| Trivial | <20 lines, single file, obvious | Execute directly |
| Small | <50 lines, 1-2 files, clear | Brief confirmation, then execute |
| Medium | 50-200 lines, 3+ files | **Offer:** "Create task file? [T/P/?]" |
| Large | >200 lines, architectural, multi-session | **Recommend:** "/plan-task for phases" |

**Behavior:**
- Trivial/Small: Proceed without asking
- Medium/Large: OFFER planning, user decides
- User says "just do it" → Treat as Trivial regardless of scope

**Offering format (Medium/Large):**
```
This seems like a {scope} task ({reason}).

[T] Create task file for better specification
[P] Proceed directly
[?] Let me ask some questions first
```

---

## 10. SELF-VERIFICATION

**AI verifies against project artifacts - user approves results, not steps.**

**Before changes, check:**

| Artifact | Question | If Conflict |
|----------|----------|-------------|
| Task Constants (🔒) | Am I modifying protected items? | 🛑 STOP - ask user |
| SOLUTION_ARCHITECTURE.md | Does change fit structure? | Adjust approach or ask |
| Tech summaries | Do I understand affected modules? | Load before coding |
| Task file (if exists) | Does change match spec? | Follow spec |

**After changes, verify:**
- Run tests → If fail, fix or report
- Check patterns match existing code style
- Lint/format if applicable

**Interrupt user ONLY when:**
- 🔒 Task Constants conflict
- Architecture conflict with no clear resolution
- Tests fail and fix is unclear
- Genuinely ambiguous requirement
- Multiple valid approaches needing preference

**DO NOT interrupt for:**
- Routine changes within understood scope
- Bug fixes with obvious solutions
- Test updates for changed code
- Refactoring that preserves behavior

---

## 11. UNDERSTAND BEFORE CODE

**AI prepares before implementing:**

**1. Requirements clarity**
- Clear → Proceed
- Ambiguous → Ask ONCE with specific questions
- Conflicting → Clarify with user

**2. Context loading**
- Load tech summary if exists (`docs/tech-summaries/`)
- If no summary → Read key source files
- Identify patterns in existing code

**3. Internal planning**
- What files to create/modify?
- What tests needed?
- Any Task Constants (🔒) to respect?

**4. Execute**
- Follow established patterns
- Write tests for new functionality
- Self-verify results

**This is preparation, not permission-seeking.**

---

## 📂 Load On Demand

| When | Read/Run |
|------|----------|
| Starting task | `docs/tasks/{component}_phase{N}_handoff.md` |
| Assessing task scope | `SOLUTION_ARCHITECTURE.md` |
| Verifying approach | `docs/tech-summaries/{layer}/{module}.md` |
| Checking constraints | Task file (if exists) |
| Writing Python | `.ai/standards/python.md` |
| Writing tests | `.ai/standards/testing.md` |
| Creating handoff | `.ai/templates/HANDOFF_TEMPLATE.md` |
| Planning complex task | Run `/plan-task` |
| Saving progress | Run `/update-context` |
| Phase complete | Run `/phase-complete` |
| Context confused | Run `/reload-context` |
| System unclear | `.ai/AGENT_REFERENCE.md` |
| Emergency | Run `/abort` |