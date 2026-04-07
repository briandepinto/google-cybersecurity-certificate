# NIST CSF Incident Analysis: DDoS ICMP Flood Attack

**Incident Type:** Distributed Denial of Service — ICMP Flood
**Root Cause:** Misconfigured firewall
**Impact:** 2-hour network outage
**Framework:** NIST Cybersecurity Framework (CSF)

---

## Overview

The organization's network experienced a two-hour outage caused by a DDoS ICMP flood attack. The attack was made possible by a misconfigured firewall that lacked IP spoofing verification rules and had no mechanism to rate-limit or block abnormal volumes of ICMP traffic. This analysis applies the five NIST CSF functions to document the incident response and establish controls to prevent recurrence.

---

## Identify

**What was identified:**

- The firewall was misconfigured — ICMP packets were not filtered and no rules existed to detect or block spoofed IP addresses.
- No network monitoring solution was in place to establish baselines or detect anomalous traffic patterns before the attack caused an outage.
- The absence of network traffic monitoring meant the attack was not detected until users began reporting connectivity loss.
- Critical systems and assets were not individually segmented, allowing the flood to affect the entire network rather than being contained.

---

## Protect

**Controls implemented or recommended:**

- **New firewall rules:** Updated firewall configuration to limit the rate of incoming ICMP packets and block packets with spoofed or unverifiable source addresses.
- **Intrusion Prevention System (IPS):** Deploy an IPS at the network perimeter capable of detecting volumetric attack signatures and automatically blocking malicious traffic in real time.
- **SIEM deployment:** Implement a Security Information and Event Management system to aggregate logs, establish normal traffic baselines, and generate alerts for anomalous conditions.
- **Network segmentation:** Segment critical systems to limit the blast radius of future volumetric attacks.

---

## Detect

**Detection capabilities established:**

- **SIEM monitoring:** Configure the SIEM to alert on abnormal ICMP traffic volumes, unusual source IP distributions, and deviations from established network baselines.
- **IPS signatures:** Enable IPS rules specifically for ICMP flood and spoofed-packet detection to provide real-time detection independent of analyst review.
- **Threshold alerting:** Set automated alerts for traffic volumes exceeding defined thresholds on any single protocol or port.

---

## Respond

**Actions taken during the incident:**

- Identified the ICMP flood as the source of the outage through log review once the attack was underway.
- Blocked all incoming ICMP echo requests at the firewall to stop the flood.
- Took non-critical network services offline to preserve bandwidth and resources for essential systems.
- Isolated affected network segments to prevent the flood from continuing to impact the full environment.
- Notified management of the outage and provided status updates throughout the two-hour incident window.

---

## Recover

**Recovery and post-incident actions:**

- Isolated affected systems and confirmed the ICMP flood had stopped before restoring services.
- Restored non-critical services in a staged manner, verifying stability before bringing each service back online.
- Conducted a full review of firewall logs and network traffic logs from the incident window to confirm the attack vector and scope.
- Reported full incident details to management, including root cause, duration, and remediation steps taken.
- Updated incident response runbooks to include ICMP flood scenarios and defined escalation procedures for future volumetric attacks.
- Scheduled a post-incident review to assess whether additional network hardening measures are required.
