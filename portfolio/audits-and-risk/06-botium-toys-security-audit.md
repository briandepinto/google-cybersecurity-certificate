# Security Audit: Botium Toys

**Organization:** Botium Toys
**Audit Type:** Internal Security Audit
**Risk Score:** 8 / 10
**Date:** [Audit Date]
**Prepared By:** Security Audit Team

---

## Scope

This audit covers Botium Toys' entire security program, including on-premises infrastructure, employee devices, internal network, systems, and data handling practices. The audit evaluates current controls against industry best practices and applicable compliance requirements.

---

## Goals

- Assess the current state of security controls at Botium Toys.
- Identify gaps in compliance with PCI DSS and GDPR requirements.
- Provide prioritized recommendations to reduce risk and improve the overall security posture.

---

## Current Assets

- On-premises equipment for in-office business functions
- Employee equipment: end-user devices, remote workstations, headsets, cables, keyboards, docking stations
- Storefront products available for retail sale and online ordering
- Systems: accounting, telecommunication, database, security, e-commerce, inventory management
- Internet access, internal network, data retention and storage
- Legacy system maintenance: end-of-life systems requiring manual monitoring

---

## Risk Assessment

**Overall Risk Score: 8/10** (High)

The high risk score reflects the combination of missing critical controls, exposure of sensitive customer payment data, and incomplete compliance with PCI DSS and GDPR requirements.

| Control | Status | Risk Contribution |
|---|---|---|
| Least privilege | Missing | High — all employees have broad data access |
| Encryption of credit card data | Missing | Critical — PCI DSS violation |
| Intrusion Detection System (IDS) | Missing | High — no detection of active attacks |
| Disaster recovery plans | Missing | High — no continuity plan exists |
| Offsite data backups | Missing | High — single point of failure |
| Strong password policy | Missing | Medium — weak credentials increase breach risk |
| Centralized password management | Missing | Medium — inconsistent enforcement |
| Firewall | In place | Mitigating |
| Antivirus software | In place | Mitigating |
| Physical security (locks, CCTV) | In place | Mitigating |
| EU GDPR 72-hour breach notification | Compliant | — |

---

## Compliance Summary

**PCI DSS:** Non-compliant. Credit card data is not encrypted and access is not restricted to authorized personnel only.

**GDPR:** Partially compliant. The 72-hour breach notification requirement is met. However, data minimization and access controls for EU customer data require improvement.

---

## Recommendations

1. **Implement least privilege:** Restrict employee data access to only what is required for their role. Conduct an access review and revoke unnecessary permissions.

2. **Encrypt cardholder data:** Apply encryption to all stored and transmitted credit card data to achieve PCI DSS compliance and protect customers.

3. **Deploy an IDS:** Implement an intrusion detection system to monitor network traffic and alert on suspicious activity.

4. **Establish disaster recovery plans:** Document and test recovery procedures for critical systems to ensure business continuity after an incident.

5. **Implement offsite data backups:** Schedule regular encrypted backups to an offsite or cloud location to protect against ransomware and hardware failure.

6. **Enforce a strong password policy:** Require minimum password length (12+ characters), complexity, and regular rotation. Enforce account lockout after repeated failed attempts.

7. **Deploy centralized password management:** Use a password manager or identity platform to enforce policy consistently and reduce credential reuse.
