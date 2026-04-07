# USB Threat Analysis: Found Drive — Hospital Parking Lot

**Scenario:** An unknown USB drive was found in a hospital parking lot.
**Owner:** Jorge Bailey, HR Manager (identified from drive contents)
**Analysis Type:** Attacker mindset + risk assessment
**Date:** [Date]
**Prepared By:** Security Team

---

## Drive Contents

Upon analysis in an isolated virtual environment, the USB drive was found to contain the following files:

| File | Type | Sensitivity |
|---|---|---|
| New hire letter | Document | Medium — contains employee PII |
| Shift schedules | Spreadsheet | Medium — reveals staffing patterns |
| Employee budget | Spreadsheet | High — contains salary and compensation data |
| Wedding guest list | Document | Low (personal) — contains personal contact information |
| Resume | Document | Low-Medium — contains personal information |
| Family photos | Images | Low (personal) |

---

## Attacker Mindset Analysis

If a malicious actor found and analyzed this drive before it was reported, the following attack vectors would be available:

### 1. Brute Force / Credential Attacks Using PII
The new hire letter and resume contain personal details about Jorge Bailey and potentially new employees (names, roles, start dates). This information can be used to construct targeted credential guessing attacks — using known formats like firstname.lastname@hospital.org combined with common password patterns derived from personal data (names, dates).

### 2. Phishing Using PII and Organizational Data
The combination of employee names, roles, and contact information from the new hire letter and guest list provides a convincing basis for spear phishing attacks. An attacker could craft highly targeted emails impersonating HR (Jorge Bailey) to other employees — requesting credential updates, payroll changes, or sensitive document submissions.

The shift schedules provide operational intelligence: an attacker knows when specific staff are on duty, which can be used to time social engineering calls or physical intrusion attempts during lower-staffing windows.

### 3. Competitor Recruiting Using Salary Data
The employee budget spreadsheet contains compensation data. A competitor or recruiter with malicious intent could use this information to target high-value employees with tailored offers, facilitating talent theft and creating operational disruption.

---

## Risk Analysis

| Risk | Likelihood | Severity | Notes |
|---|---|---|---|
| Targeted phishing using employee PII | High | High | Shift schedules and names enable highly convincing attacks |
| Credential attacks using personal data | Medium | High | PII reduces brute force search space significantly |
| Salary data leak to competitors | Medium | Medium | Reputational and operational impact |

---

## Recommendations

### 1. Disable Autorun on All Endpoints
USB drives should never autorun automatically. Disable autorun/autoplay via Group Policy on all Windows systems and equivalent settings on other platforms. This prevents malware on a found drive from executing simply by being plugged in.

### 2. Analyze Unknown Drives in a Virtual Environment Only
Any unidentified USB drive must be analyzed in an isolated virtual machine with no network access. Never insert an unknown drive into a production or network-connected system.

### 3. Encrypt Business Drives
All USB drives used for business purposes must be hardware-encrypted or use strong software encryption (AES-256). If Jorge Bailey's drive had been encrypted, the contents would be inaccessible to the finder without the decryption key.

### 4. Multi-Factor Authentication (MFA)
Enforce MFA across all hospital systems to limit the damage from credential attacks that exploit the PII exposed on this drive.

### 5. Employee Security Awareness Training
Train employees to:
- Never use personal USB drives for business data.
- Report found drives to IT security immediately without plugging them in.
- Recognize spear phishing attempts, including those impersonating HR.
- Follow data handling policies for sensitive files like payroll and staffing data.
