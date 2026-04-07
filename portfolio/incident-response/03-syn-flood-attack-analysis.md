# Cybersecurity Incident Report: SYN Flood DoS Attack

**Incident Type:** Denial of Service — SYN Flood
**Attacker IP:** 203.0.113.0
**Date:** [Incident Date]
**Prepared By:** Security Operations Team

---

## Section 1: Attack Identification

The web server began experiencing severe performance degradation and eventual unavailability. Log analysis revealed an overwhelming volume of TCP SYN requests originating from IP address `203.0.113.0`, arriving at a rate of approximately one request per millisecond. The server's connection table was exhausted, preventing legitimate users from establishing connections. This pattern is consistent with a SYN flood Denial of Service attack.

---

## Section 2: How the TCP Three-Way Handshake Works

Normal TCP connection establishment follows a three-step process:

1. **SYN:** The client sends a SYN (synchronize) packet to the server, requesting a connection.
2. **SYN-ACK:** The server acknowledges the request by sending a SYN-ACK packet back to the client and allocates resources (a half-open connection entry) while waiting for confirmation.
3. **ACK:** The client sends an ACK (acknowledge) packet to complete the handshake, and the connection is fully established.

Under normal conditions, this process completes in milliseconds and the server's resources are quickly freed or fully allocated to active connections.

---

## Section 3: How a SYN Flood Exploits the Handshake

In a SYN flood attack, the attacker sends a large volume of SYN packets but never completes the handshake — either by never sending the final ACK, or by spoofing the source IP so the SYN-ACK goes to a non-existent host.

The server allocates a half-open connection entry for each SYN received and holds it open until a timeout occurs (typically 75 seconds). When the attack rate exceeds the server's capacity to time out old entries, the connection table fills completely. At that point, the server cannot accept new legitimate connections, effectively taking the service offline.

---

## Section 4: Log Analysis Findings

Review of server logs for the incident window revealed:

- A continuous stream of SYN packets from `203.0.113.0` at approximately 1 packet per millisecond.
- No corresponding ACK packets from the source IP — confirming the handshakes were never completed.
- The server's half-open connection table reached maximum capacity within seconds of the attack beginning.
- Legitimate user connection attempts during the attack window resulted in timeouts or connection refused errors.
- No other source IPs were involved at comparable volume, indicating a single-source attack rather than a distributed (DDoS) campaign.

---

## Section 5: Recommendations

1. **SYN rate limiting:** Configure the firewall or load balancer to limit the number of SYN packets accepted per second from any single IP address. Traffic exceeding the threshold is dropped before reaching the server.

2. **Intrusion Prevention System (IPS):** Deploy an IPS capable of detecting SYN flood signatures in real time and automatically blocking offending traffic at the network perimeter.

3. **SYN cookies:** Enable SYN cookies on the web server. SYN cookies allow the server to avoid allocating connection table resources until the three-way handshake is fully completed, eliminating the half-open connection vulnerability.

4. **IP block:** Block `203.0.113.0` at the firewall immediately and monitor for the attack resuming from related IP ranges. Coordinate with the upstream ISP to apply filtering closer to the source if the attack persists.
