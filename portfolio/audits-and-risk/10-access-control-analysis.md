# Access Control Incident Analysis

**Incident:** Unauthorized Access to Payroll Systems
**Subject:** Robert Taylor Jr.
**Access Date:** October 2, 2023 — 8:29:57 AM
**Prepared By:** Security Team

---

## Incident Summary

Former contractor Robert Taylor Jr., who previously served in a legal attorney role, accessed the organization's payroll systems on October 2, 2023. His contract ended in 2019. Despite the contract termination, his account remained active and retained full administrative privileges. The unauthorized access was detected through log review.

---

## Access Event Details

| Field | Value |
|---|---|
| Subject | Robert Taylor Jr. |
| Role (former) | Contractor / Legal Attorney |
| Contract end date | 2019 |
| Access date | October 2, 2023 |
| Access time | 8:29:57 AM |
| Device | Up2-NoGud |
| Source IP | 152.207.255.255 |
| Systems accessed | Payroll systems |

---

## Root Cause Analysis

**Primary cause:** The account was never deprovisioned after the contract ended in 2019. The subject retained active credentials for approximately four years after his authorized access period ended.

**Contributing cause:** All employees and contractors were provisioned with full administrative privileges regardless of their role. There was no access control differentiation between roles, meaning a former contractor had the same level of access as an active system administrator.

**Contributing cause:** No automated account expiration policy was in place. Without a defined expiration date on contractor accounts, there was no mechanism to detect or disable stale accounts.

---

## Impact

The subject accessed payroll systems, which contain sensitive employee compensation data, banking information, and personal details. The scope of data viewed or exfiltrated requires further forensic investigation.

---

## Recommendations

### 1. Multi-Factor Authentication (MFA)
Require MFA for all user accounts, with no exceptions. Even if an attacker obtains valid credentials from a former employee, MFA prevents access without the second factor. MFA should be enforced at the identity provider level.

### 2. 30-Day Automatic Account Expiration for Contractors
All contractor accounts must be created with a hard expiration date not to exceed 30 days past the contract end date. Account expiration should be automated — the account is disabled without requiring manual action. Extension requires manager approval and formal re-provisioning.

### 3. Least Privilege for Contractors
Contractor accounts must be scoped to the minimum permissions required for their specific engagement. Legal contractors require access to legal systems only — not payroll, HR, or administrative systems. Role-based access control (RBAC) profiles should be created for common contractor roles and applied at account creation.

### 4. Quarterly Access Audits
Conduct a formal access review every quarter. All active accounts are reviewed against current employment and contract records. Any account without a corresponding active employee or contractor is disabled immediately. Accounts with privileges exceeding documented job requirements are flagged for reduction.
