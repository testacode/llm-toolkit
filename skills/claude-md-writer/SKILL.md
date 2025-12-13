---
name: claude-md-writer
description: Guide for writing and improving CLAUDE.md files following best practices. Use when creating a new CLAUDE.md, reviewing an existing one, or optimizing project documentation for Claude Code.
allowed-tools: Read, Glob, Grep, Write, Edit
---

# CLAUDE.md Writer

A skill for creating and optimizing CLAUDE.md files following industry best practices.

## When to Use This Skill

- Creating a new CLAUDE.md for a project
- Reviewing/auditing an existing CLAUDE.md
- Optimizing documentation for better Claude Code performance
- User asks about CLAUDE.md best practices

## Reference Documentation

For detailed best practices, read: `docs/claude-md-best-practices.md`

## Process

### Step 1: Analyze the Project

Before writing, gather information:

```bash
# Check project type and structure
ls -la
cat package.json 2>/dev/null || cat pom.xml 2>/dev/null || cat Cargo.toml 2>/dev/null

# Find existing documentation
ls -la docs/ 2>/dev/null
ls -la README.md 2>/dev/null
```

Identify:
- Tech stack (language, framework, build tools)
- Project structure (monorepo, single app, library)
- Existing documentation to reference

### Step 2: Apply the Three Dimensions

Every CLAUDE.md must address:

| Dimension | Question to Answer |
|-----------|-------------------|
| **WHAT** | What is this project? Tech stack? Structure? |
| **WHY** | Why does it exist? What problem does it solve? |
| **HOW** | How do I work on it? Commands? Workflows? |

### Step 3: Write Following Best Practices

**Length**: Keep under 200 lines (ideal ~100 lines)

**Structure** (in order):
1. Repository Overview (1 paragraph)
2. Why This Exists (purpose, users)
3. Quick Start & Commands (bash with descriptions)
4. Architecture Overview (key patterns)
5. Key Development Rules (with emphasis)
6. References (links to detailed docs)

**Emphasis for Critical Rules**:
```markdown
- **CRITICAL**: [Never violate this]
- **IMPORTANT**: [Always do this]
- **YOU MUST**: [Mandatory action]
```

**Progressive Disclosure**:
- Use file references instead of code snippets
- Link to external docs for detailed topics
- Keep CLAUDE.md focused on universal instructions

### Step 4: Verify with Checklist

Before finalizing, verify:

- [ ] Under 200 lines?
- [ ] Has WHAT, WHY, HOW sections?
- [ ] Critical rules have emphasis (CRITICAL/IMPORTANT)?
- [ ] Code snippets replaced with file references?
- [ ] Bash commands have descriptions?
- [ ] References external docs for detailed topics?
- [ ] No styling rules that should be in linters?

## Template

```markdown
# CLAUDE.md

This file provides guidance to Claude Code when working with this repository.

## Repository Overview

[One paragraph: what this project is, tech stack, main purpose]

## Why This Exists

[What problem it solves, who uses it, business context]

## Quick Start & Commands

\`\`\`bash
npm ci        # Install dependencies
npm start     # Start dev server
npm test      # Run tests
npm run build # Production build
\`\`\`

> **Note**: [Any important setup notes, env files, postinstall behavior]

## Architecture Overview

[Key patterns, folder structure, main concepts - keep brief]

## Key Development Rules

- **CRITICAL**: [Most important rule that must never be violated]
- **IMPORTANT**: [Second most important rule]
- [Other rules...]

## References

- `/docs/` - Detailed documentation
- `README.md` - Project readme
```

## Anti-Patterns to Avoid

| Anti-Pattern | Why It's Bad | Do This Instead |
|--------------|--------------|-----------------|
| Code snippets | Become stale, waste tokens | Use `file:line` references |
| Styling rules | LLM is slow for deterministic tasks | Configure linters |
| Kitchen sink | Dilutes instruction effectiveness | Keep < 200 lines |
| No emphasis | Critical rules same weight as minor | Use CRITICAL/IMPORTANT |
| Auto-generated | Misses project nuances | Manually craft |

## Example Improvements

### Before (Bad)
```markdown
- Don't use console.log
- Run tests
```

### After (Good)
```markdown
- **CRITICAL**: NEVER leave console.log statements in production code
- **IMPORTANT**: Always run `npm test` before pushing changes
```
