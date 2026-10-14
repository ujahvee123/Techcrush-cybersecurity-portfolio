# Incident Response Playbook: Distributed Denial-of-Service (DDoS) Attack

## Introduction
A DDoS attack overwhelms an organization's network, systems, or applications with malicious and illegitimate traffic, degrading performance and availability and preventing legitimate users from reaching the service.

## Scenario
TechCrush Group 24 hosts applications and websites for several Lagos businesses. The SOC begins receiving alerts of an unusually high volume of traffic toward the organization's public-facing cloud services, and customers report that applications are extremely slow or unavailable. Network monitoring shows a sharp increase in inbound traffic from a large number of distinct IP addresses, confirming a DDoS attack aimed at overwhelming resources and denying service to legitimate customers.

## Incident Triggers
- Sudden spike in traffic to the network/site
- Bandwidth overflow — internet link utilization over 90–100%
- Firewall overload — device CPU/memory overloaded
- Repeated connection attempts
- Unexpected degradation of network, website, application, or other critical services

## Playbook

| Section | Content |
|---|---|
| **Identification** | SOC operator monitors network alerts, the load balancer, and the network firewall continuously. When an abnormal alert appears, check bandwidth utilization and packets/requests per second. Compare against the network baseline and identify the affected IP address, domain, and application service. |
| **Detection** | Confirm the traffic increase is not actually caused by a legitimate marketing campaign, a software update, or a genuine increase in users. Determine whether the traffic is targeting the network, transport, or application layer. |
| **Containment** | Report immediately to the SOC commander and team per the security structure. Ensure critical systems and services remain protected. Cut off malicious IP addresses while maintaining availability for legitimate traffic (e.g. via upstream filtering, rate limiting, or a scrubbing/CDN service). |
| **Eradication** | Tune filtering/mitigation rules based on the observed attack signature. Close any application-layer weakness that made the attack more effective (e.g. an endpoint that was especially resource-expensive per request). |
| **Recovery** | Restore full service to legitimate users. Continue monitoring for renewed attack attempts. Review the effectiveness of the mitigation and adjust capacity/filtering as needed. |

## Why DDoS Response Looks Different From Phishing or Ransomware
There is no "disable account" or "remove malware" step here, because nothing was compromised — the organization's own systems and data remain intact. The problem is volume, not intrusion. That is exactly why a single generic incident playbook does not work across threat types: the correct first move for DDoS (traffic filtering, capacity, upstream mitigation) would do nothing for ransomware (which needs isolation), and vice versa.
