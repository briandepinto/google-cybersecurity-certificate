# SOC Alert Ticket: A-2703

**Ticket ID:** A-2703
**Severity:** Medium
**Status:** Escalated
**Assigned To:** SOC Level 1 Analyst
**Date:** January 23, 2024

---

## Alert Details

| Field | Value |
|---|---|
| Ticket ID | A-2703 |
| Alert Type | Phishing Email |
| Severity | Medium |
| Sender Domain | 76tguyhh6tgftrt7tg.su |
| Sender IP | 114.114.114.114 |
| Recipient | hr@inergy.com |
| Email Subject | Re: Infrastructure Engineer role |
| Attachment | bfsvc.exe |
| Archive Password | paradise10789 |

---

## Analysis

A phishing email was delivered to `hr@inergy.com` appearing to be a reply to a job posting for an Infrastructure Engineer role. The email originated from the domain `76tguyhh6tgftrt7tg.su` — a `.su` (Soviet Union) top-level domain, which is commonly associated with malicious activity and is a known indicator of suspicious origin.

The email contained a password-protected executable attachment, `bfsvc.exe`, with the password `paradise10789` provided in the email body. This technique is a deliberate attempt to bypass email security filters, as the archive contents cannot be scanned without the password.

**File Hash:**
`54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b`

**VirusTotal Analysis:**
The SHA-256 hash of `bfsvc.exe` was submitted to VirusTotal. The file was flagged as malicious by multiple antivirus vendors. This confirms the attachment is a known malware sample.

**Indicators of Compromise (IOCs):**
- Domain: `76tguyhh6tgftrt7tg.su`
- IP: `114.114.114.114`
- File: `bfsvc.exe`
- Hash: `54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b`

---

## Recommended Actions

1. **Quarantine the email** from the recipient's mailbox immediately.
2. **Block the sender domain** (`76tguyhh6tgftrt7tg.su`) and IP (`114.114.114.114`) at the email gateway and firewall.
3. **Verify whether the attachment was opened.** If the recipient executed `bfsvc.exe`, initiate endpoint isolation and begin malware remediation procedures.
4. **Notify the recipient** of the phishing attempt and provide guidance on reporting similar emails.
5. **Escalate to Level 2 SOC analyst** for full endpoint forensic review if execution is confirmed.
6. **Add IOCs** to the threat intelligence platform for organization-wide blocking.

---

## Disposition

Ticket escalated to Level 2 SOC analyst. Awaiting confirmation of whether the attachment was executed by the recipient.
