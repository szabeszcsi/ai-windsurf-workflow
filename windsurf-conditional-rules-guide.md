# Windsurf Conditional Rules Guide

> Task-specific rules that load on-demand, not always. Save tokens, stay focused.

---

## Quick Reference: Activation Modes

| Mode | Trigger | Use For |
|------|---------|---------|
| **Always On** | Every Cascade interaction | Core standards, project context |
| **Manual** | Type `@rule-name` in chat | On-demand specialized tasks |
| **Glob** | File pattern match | File-type specific rules |
| **Model Decision** | AI decides from description | Intent-based activation |

---

## File Structure

```
.windsurf/
└── rules/
    ├── core-standards.md        # Always On
    ├── testing.md               # Glob: **/*.test.ts, **/*.spec.ts
    ├── api-design.md            # Glob: src/api/**/*.ts
    ├── ui-components.md         # Glob: src/components/**/*.tsx
    ├── database.md              # Glob: **/migrations/*.sql
    ├── code-review.md           # Manual: @code-review
    └── refactoring.md           # Model Decision
```

---

## Rule File Anatomy

Each rule file in `.windsurf/rules/` is a markdown file with optional YAML frontmatter:

```markdown
---
trigger: glob
glob: **/*.test.ts
description: Standards for writing tests
---

# Testing Standards

- Use describe/it pattern
- Mock external dependencies  
- Meaningful test names
```

### Frontmatter Options

```yaml
---
trigger: always_on | manual | glob | model_decision
glob: <pattern>              # Required for glob trigger
description: <text>          # Required for model_decision, helpful for all
---
```

---

## Activation Mode Examples

### 1. Always On (Core Rules)

```markdown
---
trigger: always_on
description: Core project standards
---

# Project Standards

## Tech Stack
- TypeScript with strict mode
- React 18+ with hooks

## Code Style
- Early returns over nesting
- Descriptive names: isLoading, hasError
- Document public functions

## Boundaries
- Don't modify: .env*, /config/*
- Ask before major refactors
```

### 2. Glob (File-Pattern Based)

```markdown
---
trigger: glob
glob: **/*.test.ts, **/*.spec.ts
description: Testing standards
---

# Testing Rules

- Use Jest + React Testing Library
- Structure: describe → it → arrange/act/assert
- Mock external services and APIs
- Aim for behavior testing, not implementation
- Minimum 80% coverage on new code
```

**Common glob patterns:**

| Pattern | Matches |
|---------|---------|
| `*.ts` | All TypeScript files |
| `src/**/*.tsx` | All TSX files under src/ |
| `**/api/**/*.ts` | API-related TypeScript |
| `**/*.test.ts` | All test files |
| `**/migrations/*.sql` | Database migrations |
| `!**/node_modules/**` | Exclude node_modules |

### 3. Manual (@mention)

```markdown
---
trigger: manual
description: Invoke with @code-review for PR review assistance
---

# Code Review Checklist

When reviewing code, check:

## Security
- [ ] Input validation
- [ ] SQL injection prevention
- [ ] Auth/authz properly implemented

## Quality
- [ ] Error handling complete
- [ ] Edge cases covered
- [ ] No hardcoded values

## Performance
- [ ] No N+1 queries
- [ ] Proper indexing considered
- [ ] Caching where appropriate
```

**Usage:** Type `@code-review` in Cascade chat to activate.

### 4. Model Decision (AI-Triggered)

```markdown
---
trigger: model_decision
description: Apply when user asks to write, create, or generate unit tests or integration tests
---

# Test Generation Guidelines

When generating tests:

1. **Unit tests**: Test single functions in isolation
2. **Integration tests**: Test component interactions
3. **Naming**: `should_[expected]_when_[condition]`
4. **Structure**: 
   - Arrange: Set up test data
   - Act: Execute the function
   - Assert: Verify results
```

The AI reads the `description` and decides whether to apply the rule based on your prompt.

---

## Character Limits

| Scope | Limit |
|-------|-------|
| Single rule file | 12,000 characters |
| Total active rules | ~12,000 characters |
| Priority | Global → Workspace (excess truncated) |

**Strategy:** Use Glob/Manual/Model Decision to prevent all rules loading simultaneously.

---

## Best Practices

### DO ✅

- Keep Always-On rules minimal (core essentials only)
- Use bullet points and numbered lists
- Group related rules with XML tags:
  ```markdown
  <security_rules>
  - Validate all inputs
  - Use parameterized queries
  </security_rules>
  ```
- Be specific and actionable
- Version control your `.windsurf/rules/` folder

### DON'T ❌

- Add generic advice ("write clean code") - already in Cascade
- Put framework-specific details in Always-On rules
- Write long paragraphs - use structured lists
- Exceed limits - rules get truncated silently

---

## Template: Portable Rule Set

Create a reusable rules repository:

```
📁 my-windsurf-rules/
├── 📁 global/
│   └── global_rules.md           # → ~/.codeium/windsurf/memories/
├── 📁 by-task/
│   ├── testing.md
│   ├── code-review.md
│   ├── refactoring.md
│   └── documentation.md
├── 📁 by-stack/
│   ├── react-frontend.md
│   ├── node-backend.md
│   ├── python-api.md
│   └── sql-database.md
└── README.md
```

**New project setup:**
1. Copy relevant rules to `.windsurf/rules/`
2. Adjust glob patterns for project structure
3. Set appropriate activation modes

---

## Practical Example: Full-Stack Web App

```
.windsurf/rules/
├── 00-core.md                    # Always On - project basics
├── frontend-react.md             # Glob: src/components/**/*
├── frontend-styles.md            # Glob: **/*.css, **/*.scss
├── backend-api.md                # Glob: src/api/**/*
├── backend-services.md           # Glob: src/services/**/*
├── database-schema.md            # Glob: **/migrations/*, **/models/*
├── testing-unit.md               # Glob: **/*.test.ts
├── testing-e2e.md                # Glob: **/e2e/**/*
├── security-review.md            # Manual: @security
└── performance-audit.md          # Manual: @performance
```

---

## Quick Setup Checklist

- [ ] Create `.windsurf/rules/` directory in project root
- [ ] Add core Always-On rule (keep under 2000 chars)
- [ ] Identify task categories (testing, API, UI, etc.)
- [ ] Create glob-based rules for each category
- [ ] Create manual rules for on-demand tasks
- [ ] Test by working on different file types
- [ ] Commit rules to version control

---

## References

- [Official Docs: Memories & Rules](https://docs.windsurf.com/windsurf/cascade/memories)
- [Rule Templates Directory](https://windsurf.com/editor/directory)
- [Windsurf University: Creating Rules](https://windsurf.com/university/general-education/creating-modifying-rules)
