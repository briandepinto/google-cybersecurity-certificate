# PASTA Threat Model: Sneaker Marketplace Application

**Framework:** PASTA (Process for Attack Simulation and Threat Analysis)
**Application:** Sneaker resale marketplace (buyer/seller platform)
**Date:** [Date]
**Prepared By:** Security Team

---

## Stage I: Define Business Objectives

The sneaker marketplace is designed to provide a safe, trusted environment for buyers and sellers to transact. Core business objectives include:

- Provide a secure platform where buyers and sellers can transact with confidence.
- Maintain legal compliance with consumer protection, data privacy, and payment processing regulations.
- Implement a user rating and review system to establish trust between transacting parties.
- Protect user financial data and personal information.
- Prevent fraudulent listings and counterfeit products.

---

## Stage II: Define Technical Scope

**Technical components in scope:**

- **API layer:** RESTful API handling all buyer/seller interactions, listing management, and payment processing
- **Database:** SQL database storing user accounts, listings, transaction history, and ratings
- **Authentication:** SHA-256 password hashing; PKI-based certificate infrastructure for encrypted communications
- **Payment processing:** Third-party payment gateway integration
- **Front-end:** Web and mobile clients communicating with the API over HTTPS

---

## Stage III: Application Decomposition

**Data flow overview:**

1. User authenticates via the API (credentials hashed with SHA-256; session token issued)
2. Authenticated user browses listings or creates a new listing (API query to SQL database)
3. Buyer initiates purchase (API processes payment via third-party gateway)
4. Transaction recorded in database; seller notified
5. Post-transaction, both parties can submit ratings (API writes to ratings table)

*[Formal data flow diagram would be attached here in a full implementation]*

---

## Stage IV: Threat Analysis

**Threats identified:**

1. **SQL Injection:** Unsanitized input in search or listing fields could allow an attacker to manipulate database queries — exposing user data, modifying listings, or bypassing authentication.

2. **Session Hijacking:** If session tokens are not properly secured (insufficient entropy, not bound to client IP, or transmitted over insecure channels), an attacker could steal a valid session and impersonate a legitimate user.

---

## Stage V: Vulnerability Analysis

**Vulnerabilities identified:**

1. **Lack of prepared statements:** If SQL queries are constructed using string concatenation rather than parameterized queries or prepared statements, the application is vulnerable to SQL injection.

2. **Weak credential management:** If users are permitted to set short or common passwords, and if SHA-256 is used without salting, rainbow table attacks could compromise stored credentials. Additionally, weak credentials on seller accounts enable account takeover.

---

## Stage VI: Attack Modeling

**Attack tree — SQL Injection path:**

```
Goal: Access user financial data
  |
  +-- Identify injectable input field (search, listing form)
        |
        +-- Submit crafted SQL payload
              |
              +-- Bypass input validation (if absent)
                    |
                    +-- Execute malicious query
                          |
                          +-- Extract user table (accounts, payment tokens)
```

---

## Stage VII: Risk and Controls

| Risk | Control |
|---|---|
| SQL Injection | Use parameterized queries / prepared statements for all database interactions. Input validation and allowlisting on all user-supplied fields. |
| Session Hijacking | Implement MFA for all accounts. Bind session tokens to client attributes. Use secure, HttpOnly, SameSite cookies. Enforce HTTPS exclusively. |
| Credential Compromise | Continue use of SHA-256 hashing with unique per-user salts. Enforce minimum password complexity. Add MFA as second factor. |
| Incident Response | Establish a formal incident response plan covering account compromise, data breach notification, and payment fraud scenarios. |
