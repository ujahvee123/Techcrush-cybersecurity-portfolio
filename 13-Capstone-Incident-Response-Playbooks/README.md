# Capstone Project: Incident Response Playbooks

## Overview
This project was completed as part of the TechCrush Cybersecurity Track Cohort 8 capstone, developed collaboratively by an 18-person team (Group 24). It designs three incident response playbooks — phishing, ransomware, and distributed denial-of-service (DDoS), plus a reusable post-incident review template, for a fictional cloud service provider, TechCrush Group 24.

## Objective
Develop standardized, repeatable incident response procedures that let security personnel detect, contain, eradicate, and recover from real-world threats consistently, while improving coordination between the SOC, IT, management, and other teams during an active incident.

## Skills Demonstrated
Incident response lifecycle design (identification → detection → containment → eradication → recovery), threat-specific response planning, roles and escalation design, communication planning, SOC metrics (MTTD/MTTR/containment time), post-incident review process design.

## Why Three Different Playbooks, Not One Generic One
A single generic "respond to an incident" document sounds efficient but fails in practice, because phishing, ransomware, and DDoS are different enough in *mechanism* that the same response steps don't actually work for all three:

- **Phishing** is primarily an *identity* problem, the damage is stolen credentials being used elsewhere. The response centers on account containment (disable, reset, re-enable only after validation).
- **Ransomware** is primarily a *system integrity* problem — the damage is encrypted/destroyed data and possible lateral spread. The response centers on isolation first, and critically, **not shutting the system down**, since that can destroy forensic evidence still in memory.
- **DDoS** is primarily an *availability* problem — nothing is stolen or encrypted, the service is just overwhelmed. The response centers on traffic filtering and capacity, not account or endpoint containment at all.

Recognizing which *category* of damage a threat causes (confidentiality, integrity, or availability, the CIA triad again, applied to incident design) is what actually drives which playbook steps matter. This is the reasoning worth being able to explain in an interview, not just the step lists themselves.

---

## Playbook 1: Phishing Attack

### Scenario
A Cloud Operations employee at TechCrush Group 24 receives an urgent, spoofed "verify your account" email, enters credentials into a fake login page, and the SOC subsequently detects a login to that employee's cloud account from an unknown device/location.

### Incident Triggers
- Urgent, pressure-based account-verification email
- SOC alert: login from an unusual location/device
- Credentials submitted to a fake login page
- Attempts to access cloud resources using the compromised credentials

### Lifecycle Summary
| Phase | Key Actions |
|---|---|
| Identification | Flag the suspicious email; flag the unusual login/authentication event |
| Detection & Analysis | Review the email and sender domain; check if other employees received it; review auth logs for other unusual logins; identify which cloud resources were accessed |
| Containment | Disable the compromised account; terminate active sessions; block the malicious IP; watch for further suspicious activity |
| Eradication | Remove malware/malicious files via EDR; remove unauthorized accounts; reset credentials; terminate persistence mechanisms; patch the exploited weakness |
| Recovery | Restore the account only after confirming it's secure; enforce a stronger password; monitor closely; review for any remaining unauthorized changes |

### Roles
Incident Commander (coordinates, makes key decisions) → SOC Analyst (detects, escalates, investigates) → Technical Lead (handles remediation/restoration) → Communications Lead (manages internal/external communication).

### Metrics
Mean Time to Detect (MTTD), Mean Time to Respond (MTTR), Mean Time to Contain, Recovery Time, Number of Incidents.

---

## Playbook 2: Ransomware Attack

### Incident Triggers
- Administrative/account lockout anomalies
- Unfamiliar file extensions (e.g. `.lock`) or changed wallpaper
- A ransom note (typically `.txt`)
- Sudden, severe system slowdown

### Lifecycle Summary
| Phase | Key Actions |
|---|---|
| Identification | Recognize the symptom set above as consistent with ransomware |
| Detection | Review SIEM logs for mass file modification and unusual-location logins; EDR alerts on mass file renaming; helpdesk reports of inaccessible files |
| Containment | Isolate the affected system from the network; disable affected accounts; block suspected IPs; **do not shut the system down** (this destroys forensic evidence); isolate backups from the network too, so they can't be encrypted next; capture forensic images/memory where possible |
| Eradication | Search logs for IOCs; document and preserve evidence; identify and close the actual attack vector (unpatched software, weak password, phishing email); remove persistence mechanisms; quarantine and remove the ransomware; reset credentials; verify the system is clean (patch or reinstall OS) |
| Recovery | Verify backups are clean *before* restoring; restore data; test each system individually before reconnecting it to the network; monitor closely afterward |

### Why "Don't Shut It Down" Is the Single Most Important Line in This Playbook
This is the one instruction in the whole document that directly contradicts a beginner's natural instinct (turn it off to stop the damage). Shutting a compromised system down destroys volatile evidence in RAM, running processes, network connections, encryption keys, exactly the evidence a forensic investigator would need afterward to understand how the attack happened and whether it's truly contained. The correct first move is isolation (cut network access), not power-off.

### Roles & Escalation Path
Tier 1 SOC Analyst (identification) → Tier 2 SOC Analyst (confirms, hands off full log/account detail) → Incident Response Team (containment) → Eradication Team (malware removal, vector closure) → Recovery Team (restoration).

### Communication Channels
SOC-internal: secure chat. SOC → IR: incident ticket. IR → Eradication/IT: secure chat. Eradication → Recovery: incident ticket + formal handover.

### Metrics (Target Response Windows)
| Phase | Target Window |
|---|---|
| Detection | 0–15 minutes |
| Containment | 15–60 minutes |
| Eradication | 1–24 hours |
| Recovery | 24–72 hours |

---

## Playbook 3: Distributed Denial-of-Service (DDoS) Attack

### Scenario
TechCrush Group 24 hosts applications for multiple Lagos-based businesses. The SOC begins receiving alerts of an unusually high volume of inbound traffic to the public-facing cloud services, and customers report slow or unavailable applications. Traffic is confirmed to originate from a large number of distinct IP addresses.

### Incident Triggers
- Sudden traffic spike
- Bandwidth utilization at 90–100%
- Firewall/load-balancer CPU or memory overload
- Repeated connection attempts
- Degraded service availability

### Lifecycle Summary
| Phase | Key Actions |
|---|---|
| Identification | Monitor network alerts and load balancer; check bandwidth/packet/request rates against baseline; identify the affected IP, domain, and service |
| Detection | Rule out legitimate causes first (a marketing campaign, a real surge in users) before concluding it's an attack; determine which layer is being targeted (network, transport, or application) |
| Containment | Escalate to the SOC commander/team immediately; protect critical systems; block malicious IPs while preserving access for legitimate users; engage upstream mitigation (ISP/CDN/scrubbing service) as needed |
| Eradication | Tune filtering rules based on the observed attack pattern; close any application-layer weakness that made the attack more effective |
| Recovery | Restore full service; monitor for renewed attack attempts; review capacity and mitigation effectiveness |

### Why This Playbook Looks Different From the Other Two
Note that DDoS response has *no* "disable account" or "remove malware" step at all, because nothing was compromised. The organization's own infrastructure is intact; it's simply being overwhelmed by volume. This is exactly why a single generic playbook fails: applying ransomware-style containment (isolating systems) to a DDoS scenario would be pointless, while applying DDoS-style traffic filtering to a ransomware scenario would do nothing to stop encryption already in progress.

---

## Post-Incident Review Template
A reusable template was developed for after-action review of any incident type, capturing:
- Incident name/ID, date, type, and lead responder
- A plain-language summary of what happened and how it was detected
- A timeline table (date, time, event, action taken, person/team)
- What worked well
- What didn't work well (delays, gaps, communication breakdowns)
- Action items for next time, with owner, deadline, and status
- Formal sign-off (reviewer, date, signature)

**Why this matters beyond "paperwork":** an incident that's contained but never formally reviewed teaches the organization nothing. The review template is what turns a one-time response into an improvement to the *next* response, closing the loop your lesson material called "lessons learned," the final stage of the IR lifecycle.

## Conclusion
Using one common incident-response framework (identification → detection → containment → eradication → recovery) with threat-specific procedures inside it gave consistency across playbooks without forcing a one-size-fits-all response onto fundamentally different threat types. The separation of containment from eradication proved most important for ransomware specifically, account protection was the center of gravity for phishing, and rapid traffic control was the center of gravity for DDoS.

## Files
- `playbooks/phishing-ir-playbook.md`
- `playbooks/ransomware-ir-playbook.md`
- `playbooks/ddos-ir-playbook.md`
- `templates/post-incident-review-template.md`
