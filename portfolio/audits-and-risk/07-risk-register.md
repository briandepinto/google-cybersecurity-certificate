# Risk Register: Bank — Funds Asset

**Organization:** [Bank Name]
**Asset:** Funds
**Environment:** Coastal location; 100 on-premise employees, 20 remote employees; 2,000 individual accounts, 200 commercial accounts
**Date:** [Date]
**Prepared By:** Risk Management Team

---

## Risk Matrix

| Likelihood | Low (1) | Medium (2) | High (3) |
|---|---|---|---|
| **High (3)** | 3 | 6 | 9 |
| **Medium (2)** | 2 | 4 | 6 |
| **Low (1)** | 1 | 2 | 3 |

**Priority Score = Likelihood x Severity**

---

## Risk Register

| Risk | Description | Likelihood | Severity | Priority | Notes |
|---|---|---|---|---|---|
| Business email compromise | Attacker impersonates executive or vendor to initiate fraudulent wire transfer | 3 (High) | 2 (Medium) | 6 | Remote workforce increases exposure; financial transfers are high-value target |
| Compromised user database | Unauthorized access to customer account database via credential theft or SQL injection | 2 (Medium) | 2 (Medium) | 4 | 2,200 accounts represent significant breach impact; encryption and MFA reduce risk |
| Financial records leak | Sensitive financial records exposed through insider threat or misconfigured storage | 2 (Medium) | 2 (Medium) | 4 | Commercial accounts add regulatory exposure; access controls are a key mitigation |
| Theft — safe left unlocked | Physical theft of cash or negotiable instruments due to safe access control failure | 2 (Medium) | 3 (High) | 6 | Coastal location may increase physical theft risk; procedural controls critical |
| Supply chain disruption | Third-party vendor failure disrupts banking operations or data processing | 1 (Low) | 3 (High) | 3 | Coastal location adds natural disaster component; vendor SLAs and redundancy required |

---

## Priority Recommendations

### Priority 6 — Business Email Compromise
- Implement email authentication (DMARC, DKIM, SPF).
- Require out-of-band verbal confirmation for all wire transfer requests above a defined threshold.
- Train employees to recognize social engineering tactics, particularly for financial authorization requests.

### Priority 6 — Theft / Safe Left Unlocked
- Enforce dual-control procedures for safe access (two authorized employees required).
- Install CCTV monitoring at all vault and safe locations.
- Conduct regular audits of access logs.

### Priority 4 — Compromised User Database
- Apply encryption at rest for all account and PII data.
- Enforce MFA for database administrator access.
- Conduct quarterly vulnerability scans on database systems.

### Priority 4 — Financial Records Leak
- Apply least privilege to all financial record access.
- Enable audit logging on all financial system access events.
- Review and restrict cloud storage permissions for any externally accessible repositories.

### Priority 3 — Supply Chain Disruption
- Maintain an approved vendor list with documented SLAs.
- Develop a business continuity plan for critical third-party service failures.
- Identify backup vendors for high-criticality services.
