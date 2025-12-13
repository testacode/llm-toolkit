# CLAUDE.md Best Practices Guide

Reference document compiled from official sources for optimizing CLAUDE.md files in any project.

## Sources

- **Anthropic (Official)**: [Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)
- **HumanLayer**: [Writing a Good CLAUDE.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md)

---

## Core Principle

> "LLMs are stateless functions" - CLAUDE.md is the **only content automatically included** in every conversation, making it essential for onboarding agents to your codebase.

---

## The Three Dimensions

Every CLAUDE.md should address:

| Dimension | Description | Example |
|-----------|-------------|---------|
| **WHAT** | Technical stack, project structure, codebase organization | "Built with React, components in src/components/" |
| **WHY** | Project purpose, what problem it solves | "Enables users to manage their accounts" |
| **HOW** | Build tools, testing procedures, verification methods | "npm run build after changes" |

---

## Length Guidelines

| Source | Recommendation |
|--------|----------------|
| HumanLayer | < 300 lines (ideal ~60 lines) |
| Anthropic | "Concise and human-readable" (no specific limit) |
| Practical | **< 200 lines** for most projects |

### Why Length Matters

- Claude Code's system prompt contains ~50 instructions
- Research shows LLMs reliably follow ~150-200 instructions
- Each instruction in CLAUDE.md "competes" for attention
- **Bloat reduces compliance uniformly across ALL instructions**

---

## What to Include

### Essential Content (Anthropic)

```markdown
# Bash commands
- npm run build: Build the project
- npm run test: Run tests

# Code style
- Use ES modules (import/export) syntax
- Use types instead of interfaces

# Workflow
- Run tests before committing
- Run linter after code changes
```

### Recommended Sections

1. **Repository Overview** - One paragraph explaining what this is
2. **Why This Exists** - Purpose and problem it solves
3. **Quick Start & Commands** - Bash commands with descriptions
4. **Architecture Overview** - Key patterns and structure
5. **Key Development Rules** - Critical rules with emphasis
6. **References** - Pointers to detailed docs

---

## Emphasis Techniques

Use emphasis keywords for critical rules to improve adherence:

| Keyword | Usage |
|---------|-------|
| `**CRITICAL**` | Must never be violated |
| `**IMPORTANT**` | Should always be followed |
| `**YOU MUST**` | Mandatory action |
| `**Note**` | Informational callout |

### Example

```markdown
## Key Development Rules

- **CRITICAL**: NEVER commit secrets or API keys
- **IMPORTANT**: Always run tests before pushing
- **YOU MUST**: Follow the PR template when creating pull requests
```

---

## Progressive Disclosure

Instead of putting everything in CLAUDE.md, use **references**:

### Do This

```markdown
### Component Structure

Reference implementation: `src/components/Button/Button.tsx`

Key patterns:
- Props defined as types
- Styles co-located with component
```

### Avoid This

```markdown
### Component Structure

interface ButtonProps {
  label: string;
  onClick: () => void;
  variant?: 'primary' | 'secondary';
}

export const Button: React.FC<ButtonProps> = ({ label, onClick, variant = 'primary' }) => {
  return (
    <button className={`btn btn-${variant}`} onClick={onClick}>
      {label}
    </button>
  );
};
```

### Why?

- Code snippets become stale; file references stay current
- Reduces token consumption
- Claude can read the actual file when needed

---

## File Placement Strategy (Anthropic)

| Location | Use Case |
|----------|----------|
| **Root directory** | Most common, team-shared via git |
| `CLAUDE.local.md` | Local-only (add to .gitignore) |
| **Parent directories** | Monorepos - auto-loaded from parents |
| **Child directories** | On-demand when working in that area |
| `~/.claude/CLAUDE.md` | Global, applies to all sessions |

---

## What NOT to Include

### 1. Styling Rules (Use Linters Instead)

> "Never send an LLM to do a linter's job" - HumanLayer

**Bad**: Including indentation rules, naming conventions in CLAUDE.md

**Good**: Configure ESLint/Prettier/Stylelint and let pre-commit hooks enforce

### 2. Task-Specific Details

Don't include instructions that only apply to specific scenarios:
- Database schema guidance (unless every task touches DB)
- Deployment procedures (reference external docs instead)
- One-off workarounds

### 3. Auto-generated Content

CLAUDE.md is "the highest leverage point" - manually craft it, don't auto-generate.

---

## Optimization Techniques

### 1. Iterative Refinement

Treat CLAUDE.md like a prompt you'd improve:
- Test if instructions are followed
- Add emphasis where needed (`IMPORTANT`, `CRITICAL`)
- Remove instructions that aren't followed anyway

### 2. Dynamic Updates

Press `#` key during Claude Code sessions to automatically incorporate instructions.

### 3. Team Collaboration

Include CLAUDE.md changes in commits so teammates benefit from accumulated knowledge.

---

## Common Anti-Patterns

| Anti-Pattern | Problem | Solution |
|--------------|---------|----------|
| Kitchen sink | Too many instructions dilute effectiveness | Keep < 200 lines |
| Code snippets | Become stale, waste tokens | Use file:line references |
| Styling rules | LLM is slow/expensive for deterministic tasks | Use linters |
| No emphasis | Critical rules get same weight as minor ones | Use CRITICAL/IMPORTANT |
| No WHY section | Agent doesn't understand project context | Add purpose explanation |

---

## Quick Checklist

Before committing CLAUDE.md changes:

- [ ] Under 200 lines?
- [ ] Has WHAT, WHY, HOW sections?
- [ ] Critical rules have emphasis (CRITICAL/IMPORTANT)?
- [ ] Code snippets replaced with file references?
- [ ] Bash commands have descriptions?
- [ ] References external docs for detailed topics?
- [ ] No styling rules that should be in linters?

---

## Template Structure

```markdown
# CLAUDE.md

Brief intro about Claude Code guidance.

## Repository Overview

One paragraph: what this project is and tech stack.

## Why This Exists

What problem it solves, who uses it.

## Quick Start & Commands

\`\`\`bash
npm ci        # Install dependencies
npm start     # Dev server
npm run build # Production build
npm test      # Run tests
\`\`\`

> **Note**: Any important setup notes (e.g., postinstall behavior, env files).

## Architecture Overview

Key patterns, folder structure, main concepts.

## Key Development Rules

- **CRITICAL**: [Most important rule]
- **IMPORTANT**: [Second most important]
- Other rules...

## References

- `/docs/architecture/` - Detailed architecture
- `/docs/development/` - Development guides
```

---

*Last updated: 2024-12-01*
