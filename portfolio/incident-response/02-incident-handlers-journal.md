# Incident Handler's Journal

**Analyst:** Brian De Pinto
**Organization:** Security Operations Center

---

## Entry 001

**Date:** January 16, 2024
**Entry:** 001
**Description:** Ransomware attack

A small US healthcare clinic experienced a ransomware attack. Employees reported being unable to access files and received a ransom note demanding payment in exchange for a decryption key. Investigation determined the initial vector was a phishing email containing a malicious attachment. An employee opened the attachment, which executed the ransomware payload and began encrypting files across the network.

**The 5 W's:**
- **Who:** Unknown external threat actor
- **What:** Ransomware deployment via malicious email attachment
- **When:** Business hours, January 16, 2024
- **Where:** Healthcare clinic internal network
- **Why:** Financial extortion

**Tools used:** None at this stage.

**Notes:** Healthcare organizations are high-value ransomware targets due to urgency of patient care operations and sensitivity of records. Employee phishing awareness training is a critical control gap.

---

## Entry 002

**Date:** January 23, 2024
**Entry:** 002
**Description:** Phishing alert investigation — Ticket A-2703

Received a medium-severity phishing alert (Ticket A-2703) for investigation. The alert flagged a suspicious email sent to an employee. The email contained an attachment with a file hash of:

`54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b`

**Tool used:** VirusTotal

Submitted the hash to VirusTotal for analysis. Results confirmed the file is malicious — flagged by multiple antivirus vendors as a known malware sample. Based on this finding, the alert was escalated to a Level 2 SOC analyst for further action, including endpoint isolation and user notification.

**Outcome:** Escalated to L2 SOC analyst. Ticket updated with VirusTotal findings.

---

## Entry 003

**Date:** January 24, 2024
**Entry:** 003
**Description:** Data theft investigation

Investigated a data theft incident. Review of historical records indicated the affected employee received a ransom email on December 22, 2022. Network traffic analysis was performed to identify any exfiltration channels and understand the scope of data potentially stolen.

**Tool used:** Wireshark

Analyzed packet captures from the relevant timeframe. Wireshark was used to filter traffic by IP and protocol to identify suspicious outbound connections. Analysis of the captures revealed evidence consistent with data exfiltration activity prior to the ransom email being received.

**Notes:** Wireshark is effective for deep packet inspection but time-consuming at scale. SIEM integration would improve detection speed for future incidents.

---

## Entry 004

**Date:** January 29, 2024
**Entry:** 004
**Description:** Chronicle SIEM — phishing domain investigation

Used Chronicle SIEM to investigate a phishing domain identified in a separate alert. Chronicle's domain intelligence and asset timeline views were used to trace activity associated with the suspicious domain.

**Tool used:** Chronicle SIEM

**Findings:**
- The domain was linked to credential theft activity.
- Chronicle logs showed 6 POST requests to `/login.php` from internal hosts, indicating successful phishing — users were submitting credentials to the attacker-controlled site.
- Asset search in Chronicle revealed 2 additional related domains operating in the same campaign, both with similar infrastructure signatures.

**Outcome:** All 3 domains blocked at the firewall. Affected user accounts flagged for mandatory password reset. Findings documented and forwarded to the threat intelligence team for broader campaign tracking.
