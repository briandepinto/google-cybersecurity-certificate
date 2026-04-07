# Security Risk Assessment: Network Hardening Recommendations

**Prepared By:** Security Analyst
**Date:** [Date]

---

## Part 1: Hardening Tools Selected

After reviewing the organization's current network security posture, the following three hardening measures are recommended for immediate implementation:

1. Multi-Factor Authentication (MFA)
2. Strong Password Policies
3. Firewall Port Filtering

These three controls address the highest-priority attack vectors — credential compromise, brute force attacks, and unauthorized network access — and can be implemented without significant infrastructure changes.

---

## Part 2: Explanation and Justification

### 1. Multi-Factor Authentication (MFA)

**What it is:** MFA requires users to verify their identity using two or more factors — typically something they know (password) and something they have (authenticator app, hardware token) or something they are (biometric).

**Why it was selected:** Passwords alone are insufficient protection. Phishing attacks, credential stuffing, and brute force can all result in password compromise. MFA ensures that even a stolen password cannot grant access without the second factor.

**Implementation requirements:**
- MFA is required for all administrator and privileged accounts without exception.
- Authenticator app-based MFA (TOTP) is preferred over SMS-based MFA, which is vulnerable to SIM swapping.
- MFA should be enforced at the identity provider level to cover all authenticated access points, including VPN, admin consoles, and cloud portals.

---

### 2. Password Policies

**What it is:** A formalized set of requirements governing how passwords are created, managed, and protected across the organization.

**Why it was selected:** Weak, reused, or shared passwords remain one of the most common causes of unauthorized access. A strong password policy eliminates the most easily exploitable credential vulnerabilities.

**Policy requirements:**
- Minimum password length: 12 characters.
- Complexity requirements: must include uppercase letters, lowercase letters, numbers, and special characters.
- Account lockout: accounts are locked after 5 consecutive failed login attempts. Lockout duration: 30 minutes, or until reset by an administrator.
- Password reuse: users may not reuse any of their last 10 passwords.
- Password sharing: explicitly prohibited. Each user must have unique credentials.
- Passwords must be stored using a strong hashing algorithm (bcrypt or equivalent) — plaintext or reversibly encrypted storage is prohibited.

---

### 3. Firewall Port Filtering

**What it is:** Firewall rules that control which network ports are open and which traffic is permitted to traverse the network boundary, based on an allowlist of known legitimate traffic.

**Why it was selected:** Unnecessary open ports expand the attack surface. An attacker who discovers an open port with a vulnerable or misconfigured service can use it as an entry point. Closing unused ports and restricting traffic to known-good patterns significantly reduces exposure.

**Implementation requirements:**
- Conduct a full audit of currently open ports and identify all services running on each.
- Close all ports that do not serve a current, documented business need.
- Implement an allowlist: only traffic from approved source IPs on approved ports is permitted inbound.
- Rules are reviewed and audited quarterly. Any new service requiring an open port must go through a formal change control process before the port is opened.
- Outbound filtering should also be configured to prevent unauthorized data exfiltration over non-standard ports.
