---
name: product
description: Ensure features are well-scoped and delivered with quality. Use when defining requirements, writing acceptance criteria, reviewing scope, or closing a feature. Invoke when the user asks "what should this do", "is this in scope", or before starting any implementation.
---

# Product

## Before Starting Any Feature
- Is there a clear problem statement?
- Who is the user and what is their goal?
- What are the acceptance criteria? (specific and testable)
- What is explicitly out of scope?
- Are there dependencies on other systems?

## Acceptance Criteria Format
```
Given [context]
When [action]
Then [expected outcome]
```

## Scope Control
- If a task grows during implementation, stop and reassess
- New discoveries go into backlog — don't expand scope mid-sprint
- Document scope changes explicitly if they must happen now

## Definition of Done
- Feature works according to acceptance criteria
- Tests written and passing
- No known bugs introduced
- Documentation updated if applicable
- Reviewed by at least one other person

## Changelog
- Every user-facing change gets a changelog entry
- Format: `[type] Short description` — types: Added, Changed, Fixed, Removed, Security
- Audience: end user, not developer
