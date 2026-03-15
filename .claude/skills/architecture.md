---
name: architecture
description: Guide structural decisions before coding. Use when starting a new feature, proposing a new module, evaluating design trade-offs, or documenting architectural decisions (ADRs). Invoke when the user asks "how should I structure this", "what pattern should I use", or before any significant implementation begins.
---

# Architecture

## Principles
- Prefer simplicity over cleverness
- Design for change: loose coupling, high cohesion
- Explicit over implicit dependencies
- Document decisions as ADRs (Architecture Decision Records)
- Validate assumptions before implementing

## Before Starting Any Feature
1. Understand the full scope — what changes, what doesn't
2. Identify integration points with existing modules
3. Consider failure scenarios
4. Propose the simplest solution that solves the problem
5. Get alignment before writing code

## ADR Format
```
## ADR-[N]: [Title]
**Status**: Proposed | Accepted | Deprecated
**Context**: Why this decision is needed
**Decision**: What was decided
**Consequences**: Trade-offs and implications
```

## Patterns to Prefer
- Layered architecture: clear separation of concerns
- Repository pattern for data access
- Dependency injection for testability
- Event-driven for async/decoupled flows
- API-first design for integrations

## Patterns to Avoid
- God objects / monolithic functions
- Circular dependencies
- Business logic in infrastructure layer
- Hardcoded configuration
- Premature optimization
