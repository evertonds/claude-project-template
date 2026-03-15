---
name: integrations
description: Apply standards for integrating with external APIs and third-party services. Use when calling external APIs, implementing OAuth flows, handling webhooks, or designing retry/fallback logic. Invoke when the user mentions Salesforce, Stripe, third-party APIs, webhooks, or any external service integration.
---

# Integrations

## Before Integrating
- Read the API documentation fully before writing code
- Understand rate limits, quotas, and SLA of the external service
- Define what happens when the integration is unavailable (graceful degradation)
- Check if an official SDK exists — prefer it over raw HTTP

## Authentication
- OAuth 2.0: implement token refresh proactively (before expiry, not on failure)
- API keys: store in secret manager, never in code or committed env files
- Service accounts: scope to minimum required permissions

## Resilience
- Implement retry with exponential backoff for transient errors
- Define timeout for every external call — never leave it unbounded
- Circuit breaker pattern for critical integrations
- Distinguish retryable errors (5xx, timeout) from non-retryable (4xx)

## Idempotency
- Design integration calls to be safely retryable
- Use idempotency keys when the API supports them
- Log external call attempts with enough context to deduplicate

## Webhooks
- Validate webhook signatures before processing
- Respond with 2xx immediately — process asynchronously
- Implement deduplication (at-least-once delivery)
- Log raw payload before processing

## Data Contracts
- Document expected request/response schema for each integration
- Validate response schema — don't assume external APIs are stable
- Monitor for breaking changes (deprecation notices, API changelogs)

## Testing Integrations
- Mock external calls in unit and integration tests
- Use sandbox/test environments in staging
- Never call production third-party APIs from test suites
