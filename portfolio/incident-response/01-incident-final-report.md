# Incident Final Report

**Incident:** Forced Browsing Attack — Customer Data Exposure
**Date of Incident:** December 28, 2022
**Report Date:** January 2023
**Prepared By:** Security Operations Team

---

## Executive Summary

On December 28, 2022, an attacker exploited a forced browsing vulnerability in the company's e-commerce web application to access the purchase confirmation pages of approximately 50,000 customers. The attacker systematically modified order numbers in URLs to enumerate and retrieve other customers' transaction data, including names, email addresses, and partial payment information. The estimated financial impact is $100,000, accounting for regulatory notification costs, legal exposure, and remediation expenses. This report documents the timeline, investigation findings, response actions taken, and recommendations to prevent recurrence.

---

## Timeline

| Date/Time | Event |
|---|---|
| Dec 28, 2022 — ~06:00 | Attacker begins enumerating order confirmation URLs |
| Dec 28, 2022 — ~11:00 | Anomalous traffic volume detected in web server logs |
| Dec 28, 2022 — 13:45 | Security team notified; investigation initiated |
| Dec 28, 2022 — 14:30 | Affected endpoint isolated; access restricted |
| Dec 28, 2022 — 17:00 | Scope confirmed: 50,000 customer records accessed |
| Dec 29, 2022 | Customer notification process initiated |
| Jan 2023 | Remediation deployed; penetration test scheduled |

---

## Investigation

**Attack Vector:** Forced browsing via URL parameter manipulation. The e-commerce application exposed order confirmation pages at predictable URLs in the format `/order/confirmation?id=XXXXXX`. No authentication or authorization check was enforced on these pages — any user who knew (or could guess) a valid order number could view the associated customer record.

**Method:** The attacker automated sequential requests, incrementing the order ID parameter with each request. Each successful response returned the customer's name, email address, shipping address, and partial payment information.

**Scope:** Approximately 50,000 customer records were accessed over a five-hour window before detection. Server logs confirmed the volume and pattern of requests originating from a single IP address.

**Financial Impact:** Estimated at $100,000, including breach notification obligations, legal counsel, regulatory exposure, and engineering remediation time.

---

## Response and Remediation

1. **Immediate containment:** Access to order confirmation pages was restricted while the vulnerability was patched.
2. **Customer notification:** Affected customers were notified in accordance with applicable data breach notification requirements.
3. **Access control patch:** Authentication checks were added to all order confirmation endpoints, ensuring only the authenticated account holder can view their own order data.
4. **Log review:** Full server logs for the affected window were preserved and reviewed to confirm the scope of the breach.

---

## Recommendations

1. **URL allowlisting:** Implement allowlists that restrict which URL patterns and parameter values are accepted. Requests outside expected patterns should be rejected with a 403 response.

2. **Authenticated access controls:** All pages displaying customer-specific data must verify that the authenticated session matches the resource being requested. Implement server-side authorization checks — do not rely on obscurity of order IDs.

3. **Routine penetration testing:** Conduct scheduled penetration tests at least annually, with additional tests following any significant application changes. Forced browsing and IDOR (Insecure Direct Object Reference) vulnerabilities should be explicitly included in the test scope.

4. **Rate limiting:** Apply rate limiting to order lookup endpoints to detect and block enumeration attempts automatically.

5. **Anomaly alerting:** Configure automated alerts for abnormal request volumes to any single endpoint to reduce detection time in future incidents.
