---
name: security
description: Apply security best practices across all layers. Use this skill on every feature, API endpoint, authentication flow, data handling task, or whenever dealing with user input, permissions, secrets, or external integrations. Invoke proactively — security is transversal and should not wait to be asked.
---

# Security

## Non-Negotiables
- Never hardcode secrets, tokens, passwords, or API keys in code
- Secrets always via environment variables or secret managers
- Never log sensitive data: tokens, passwords, PII, financial data
- Never commit `.env` files — ensure `.gitignore` covers them

## Authentication & Authorization
- Always validate authentication on the backend — never trust frontend alone
- Implement authorization checks at the function/service level, not just routes
- Use principle of least privilege for all roles and permissions
- Multi-tenant systems: always filter by tenant identifier — never expose cross-tenant data
- Define token expiration and refresh strategies upfront

## Input Validation
- Validate and sanitize all inputs at the entry point
- Use parameterized queries / ORM — never raw string interpolation in SQL
- Validate file uploads: type, size, and content
- Reject unexpected fields in API payloads (strict schema validation)

## API Security
- Rate limiting on all public endpoints
- CORS configured explicitly — never wildcard `*` in production
- HTTPS only in production
- Sensitive operations require re-authentication or confirmation

## Dependencies
- Never install packages without verifying source and maintenance status
- Regularly check for known vulnerabilities (`pip audit`, `npm audit`)
- Pin dependency versions in production

## Audit & Logging
- Log security-relevant events: login, permission denied, data export, admin actions
- Logs must include: timestamp, user/session id, action, resource — never the sensitive value itself

## OWASP Top 10 Awareness
Always consider: Injection, Broken Auth, Sensitive Data Exposure, Broken Access Control,
Security Misconfiguration, XSS, Insecure Deserialization, Known Vulnerabilities, Insufficient Logging.
