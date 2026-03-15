---
name: documentation
description: Ensure projects and modules are understandable without the author present. Use when writing READMEs, ADRs, runbooks, docstrings, or changelogs. Invoke when the user finishes a module, closes a feature, or asks how to document something.
---

# Documentation

## Mandatory Docs per Project
- `README.md`: what it is, how to run, how to deploy, how to contribute
- `CHANGELOG.md`: user-facing changes per version
- `docs/decisions/`: ADRs for significant architectural decisions
- `docs/runbooks/`: operational procedures (deploy, rollback, incident response)

## README Structure
```
# Project Name
One-line description.

## Overview
## Stack
## Getting Started
## Environment Variables
## Architecture
## Contributing
```

## Code Documentation
- Document the *why*, not the *what*
- Public functions/classes: docstrings always
- Complex logic: inline comment explaining the reasoning
- Avoid obvious comments

## Diagrams
- Use text-based diagrams when possible (Mermaid, PlantUML) — they live in git
- Update diagrams when architecture changes — stale diagrams are worse than none

## Runbook Format
1. When to use this runbook
2. Prerequisites
3. Step-by-step instructions
4. Expected outcome
5. Rollback if something goes wrong

## Documentation Debt
- Missing docs for a critical module = a bug
- When touching old code, improve its docs as part of the task
