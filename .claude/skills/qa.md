---
name: qa
description: Apply testing strategy and quality standards. Use when writing tests, reviewing test coverage, validating a feature before merge, or when the user asks about test structure, test types, or how to test a specific scenario.
---

# QA

## Testing Pyramid
- **Unit**: fast, isolated, majority of tests — mock external dependencies
- **Integration**: test modules working together — real DB (test instance), mocked external APIs
- **E2E**: critical user flows only — expensive, run on CI

## Before Modifying Existing Code
1. Identify all files that depend on the module
2. Run existing tests to establish baseline
3. Make the change
4. Run tests again — no regression allowed
5. Add/update tests to cover the change

## Test Quality Standards
- Test behavior, not implementation
- Each test: one assertion focus
- Test names describe the scenario: `test_should_return_404_when_user_not_found`
- Cover: happy path, edge cases, failure/error scenarios
- No flaky tests — fix or delete

## Coverage Guidelines
- Business-critical functions: 100% coverage required
- Core utilities and services: > 80%
- Don't chase % — test what matters

## API Contract Testing
- Document request/response contracts explicitly
- Any breaking change requires version bump
- Validate response schemas in integration tests

## Before Merging
- All tests passing
- No skipped tests without documented reason
- Coverage not decreased from baseline
- New features have corresponding tests
