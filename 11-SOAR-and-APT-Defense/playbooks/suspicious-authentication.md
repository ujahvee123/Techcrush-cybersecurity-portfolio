# PLAYBOOK: Suspicious Authentication

## TRIGGER
High-confidence suspicious authentication alert.

## STEPS
1. Extract username.
2. Extract source IP.
3. Check source IP reputation against threat intelligence.
4. Search SIEM for previous authentication events involving this user or IP.
5. Search for activity involving the same username across other hosts.
6. Check endpoint activity for the affected host.
7. Check for persistence mechanisms (scheduled tasks, new services).
8. Check for lateral movement (authentication attempts against other hosts).
9. Check for unusual outbound traffic.
10. Calculate investigation priority based on findings.
11. Create incident ticket.
12. Escalate to SOC analyst for human review.

## OPTIONAL RESPONSE
Recommend account containment or host isolation.

## APPROVAL GATE
Human analyst approval required before any disruptive containment action
(disabling accounts, isolating hosts) is executed.
