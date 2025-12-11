---
name: spawn-agent
description: Protocol for invoking and managing specialized sub-agents. Usage: /spawn-agent
auto_execution_mode: 0
---

# Spawn Agent Workflow

> **Note:** Native Claude Code subagents (`.claude/agents/`) now auto-invoke based on task context. This workflow is kept for reference.

Full protocol for invoking and managing sub-agents.

---

## Overview

Agents are specialized AI roles that focus on specific tasks (review, architecture, testing, etc.). This workflow describes how to spawn, configure, and manage them.

---

## Step 1: Choose Agent Type

| Agent | When to Use | Command |
|-------|-------------|---------|
| Reviewer | Code review, quality checks | `/spawn-reviewer` |
| Architect | Design decisions, structure | `/spawn-architect` |
| Tester | Test generation, coverage | `/spawn-tester` |
| Implementer | Code writing tasks | (coordinator spawns) |
| Coordinator | Multi-agent orchestration | (complex tasks) |

---

## Step 2: Prepare Context

Before spawning, gather:

### Required
- **Scope**: What files/feature to work on
- **Task**: Clear description of what agent should do
- **Constraints**: Any limitations (time, scope, style)

### Optional
- **Priority**: HIGH / MEDIUM / LOW
- **Expected output**: Format preferences
- **Handoff context**: If continuing from another agent

---

## Step 3: Invoke Agent

### Via Slash Command (Recommended)
```
/spawn-reviewer
```

### Via Explicit Request
```
Act as the Reviewer agent.
Read .ai/agents/reviewer.md for your role.
```

### With Context
```
/spawn-reviewer

Scope: src/auth/ directory
Task: Review the new OAuth implementation
Priority: HIGH
Focus: Security and error handling
```

---

## Step 4: Agent Activation

When activated, agent will:

1. **Load role definition** from `.ai/agents/{agent-name}.md`
2. **Read context** from `dev_context.md`
3. **Confirm understanding** of task scope
4. **Check for Task Constants** (will not modify)
5. **Begin work** within defined boundaries

---

## Step 5: Monitor Agent

### Status Tracking

Check agent status:
```
/agent-status
```

### In dev_context.md

```markdown
## Active Agents

| Agent | Status | Task | Started |
|-------|--------|------|---------|
| Reviewer | Working | OAuth review | 10:30 |
```

---

## Step 6: Handle Output

### Standard Agent Output Format

```markdown
## {Agent} Analysis

**Scope:** {what was analyzed}
**Files:** {list of files}

### Findings
{numbered list}

### Recommendations
{actionable items}

### Out of Scope
{what was NOT checked}

### Handoff
{if another agent needed}
```

### After Agent Completes

1. Review findings
2. Accept/reject recommendations
3. Update `dev_context.md` if needed
4. Process any handoff requests

---

## Step 7: Agent Handoff

When one agent needs another:

```markdown
### Handoff to {Next Agent}

**Reason:** {why needed}
**Context:** {what they need}
**Files:** {relevant paths}
**Priority:** HIGH/MEDIUM/LOW
```

User decides whether to spawn the next agent.

---

## Agent Behavior Rules

### Agents MUST:
- Stay within defined role boundaries
- Use structured output format
- Preserve context (file:line references)
- Declare what they did NOT check

### Agents MUST NOT:
- Modify Task Constants
- Commit code without permission
- Override another agent's findings
- Work outside their expertise

---

## Spawning Multiple Agents

### Sequential (Default)
```
1. Spawn Architect for design
2. Review output, approve
3. Spawn Implementer for code
4. Review output, approve
5. Spawn Tester for tests
```

### Parallel (Via Coordinator)
```
For complex tasks, spawn Coordinator agent:
/spawn-coordinator

Coordinator will orchestrate multiple agents.
See: .ai/agents/coordinator.md
```

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Agent working outside scope | Re-read role file, clarify boundaries |
| Output format wrong | Remind of structured output requirement |
| Conflict with another agent | See `.ai/coordination/conflict-resolution.md` |
| Context getting large | `/check-status`, consider new session |
| Agent stuck | `/agent-status`, provide clarification |

---

## Related Files

- Agent definitions: `.ai/agents/`
- Coordination patterns: `.ai/coordination/`
- Multi-developer: `.ai/multi-dev/`
- Agent protocol: `.ai/agents/_agent-protocol.md`
