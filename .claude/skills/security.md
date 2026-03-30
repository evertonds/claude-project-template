---
name: security
description: Apply security best practices across all layers. Use this skill on every feature, API endpoint, authentication flow, data handling task, or whenever dealing with user input, permissions, secrets, or external integrations. Invoke proactively — security is transversal and should not wait to be asked.
---

# Security

## 1. Universal Rules (always apply)

- Never log PII in application or debug logs. In audit logs, use unique identifiers (UUIDs) to track who did what — never expose personal data in plain text.
- Never hardcode secrets, tokens, passwords, or API keys — always use environment variables or a secret manager
- Never commit `.env` files — ensure `.gitignore` covers them
- Validate and sanitize all external inputs at the entry point (user input, API payloads, file uploads, query strings)
- Enforce authentication before any data access — never trust frontend-only validation
- Use parameterized queries / ORM — never raw string interpolation in SQL
- Use principle of least privilege for all roles and permissions

### OWASP Top 10 Checklist

Apply this checklist on every task that touches the areas below:

| Area | Controls to verify |
|---|---|
| Auth flows | Broken Auth (A07), Security Misconfiguration (A05) |
| Data access | Broken Access Control (A01), Sensitive Data Exposure (A02) |
| File upload | Insecure Deserialization (A08), validate type, size, and content |
| External integrations | Injection (A03), Known Vulnerabilities (A06), SSRF (A10) |

---

## 2. Multi-tenancy Rules

<!-- Configure in CLAUDE.md: MULTI_TENANT=true/false -->
<!-- If MULTI_TENANT=false, this section is informational only. -->

- Every query that accesses tenant-scoped data **must** filter by tenant identifier
- Tenant identifier **must** come from the authenticated token — never from user input or request body
- Never expose or leak data from one tenant to another
- Isolation must be enforced at the service/repository layer, not just at the route layer
- Log cross-tenant access attempts as security events

---

## 3. SAST Gate

<!-- Configure in CLAUDE.md: SECURITY_TOOL -->
<!-- Set the tool and run command for this project's stack. -->

- Run SAST before every commit (invoked by `/task-done` Gate 2)
- Block on any finding with severity **HIGH** or **CRITICAL** — do not commit until resolved
- Downgrading severity to bypass the gate is not allowed

### Examples by stack (reference — configure the actual command in CLAUDE.md)

```
# Python
bandit -r ./src

# Node / TypeScript
njsscan . && npm audit

# TypeScript (type check)
tsc --noEmit

# Go
gosec ./...
```

---

## 4. Project-Specific Rules

<!-- Fill in the fields below in this project's CLAUDE.md under "Security Setup". -->
<!-- This section is intentionally empty in the template. -->

- **Authentication method:** <!-- ex: JWT / session cookie / OAuth2 -->
- **Authorization model:** <!-- ex: RBAC / ABAC / row-level security -->
- **Sensitive data types in this project:** <!-- ex: CPF, CREA, bank account numbers -->
- **Known attack vectors for this domain:** <!-- ex: IDOR on resource IDs, price tampering, privilege escalation via role endpoint -->
