---
name: privacy
description: Apply privacy-by-design principles and LGPD compliance rules across all data handling tasks. Use this skill whenever a task touches personal data, user records, data collection, storage, deletion, or any regulatory requirement. Invoke proactively — privacy is transversal and must not be an afterthought.
---

# Privacy

## 1. Universal Rules (always apply)

- Classify every data field before implementing storage or processing:

  | Class | Definition |
  |---|---|
  | `PUBLIC` | No restrictions — freely shareable |
  | `INTERNAL` | Internal use only — not for external exposure |
  | `PERSONAL` | Identifies or relates to a natural person (name, email, phone, IP) |
  | `SENSITIVE` | Special categories under Art. 5, IX LGPD (health, biometrics, political opinion, etc.) |

- Never log personal data: name, email, CPF, phone number, address, or any field classified `PERSONAL` or `SENSITIVE`
- Mask personal data in any debug output, error messages, or stack traces — show only a truncated or hashed representation
- Data minimization: collect only what is strictly necessary for the stated purpose
- Prefer soft delete (mark as deleted, retain for retention period) over immediate hard delete for records containing personal data
- Encryption at rest is mandatory for fields classified `SENSITIVE`

---

## 2. Retention Rules

<!-- Configure in CLAUDE.md: RETENTION -->
<!-- Define the retention period per data category for this project. -->

- Each data category must have an explicit retention period defined in the project's CLAUDE.md
- After the retention period expires, personal data must be deleted or anonymized
- Deletion must cascade to all related personal data records (linked tables, audit logs, backups in scope)
- Anonymization is only valid if re-identification is technically infeasible

### Reference retention periods (configure the actual values in CLAUDE.md)

```
# Examples — do not use as-is
Employee records:    contract duration + 5 years (labor law)
Customer data:       contract duration + 5 years
Financial records:   5 years (Lei 9.430/96)
Consent records:     retain while consent is active + evidence of revocation
```

---

## 3. Legal Basis

<!-- Configure in CLAUDE.md under "Privacy Setup". -->
<!-- This section is intentionally empty in the template. -->
<!-- LGPD (Lei 13.709/2018) requires an explicit legal basis for every processing activity. -->

- **Legal basis for personal data processing:**
  <!-- Options: contract / consent / legitimate interest / legal obligation -->
  <!-- Art. 7 LGPD — select the applicable basis for this project -->

- **Sensitive data categories present (Art. 5, IX LGPD):**
  <!-- ex: health data, biometric data, racial/ethnic origin, political opinion, religious belief -->
  <!-- If none, state: none -->

- **Data subjects:**
  <!-- Who the personal data belongs to -->
  <!-- ex: employees / customers / third parties / minors -->

- **Regulatory bodies applicable:**
  <!-- Which authorities oversee this project's domain -->
  <!-- ex: ANPD / IBAMA / ANM / FEAM / IEF -->

---

## 4. Project-Specific Rules

<!-- Fill in the fields below in this project's CLAUDE.md under "Privacy Setup". -->
<!-- This section is intentionally empty in the template. -->

- **PII fields in this project:** <!-- ex: nome, email, CPF, CREA, cargo, telefone -->
- **Encryption requirements:** <!-- ex: CPF and CREA encrypted at rest with AES-256 -->
- **Consent flow implemented:** <!-- ex: yes — opt-in on registration, stored in consents table -->
- **Data deletion flow implemented:** <!-- ex: soft delete on User, cascade to related PersonalInfo -->
