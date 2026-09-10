# SOC Alert Triage

| Alert | Severity | Initial Assessment | Action |
|---|---|---|---|
| ALERT-001 | Low | Routine security tool activity, no attacker involvement implied | Document/Close |
| ALERT-002 | Medium | Repeated authentication failures; attack attempt, outcome unknown | Investigate |
| ALERT-003 | Informational | Normal login activity, no anomaly indicated | Close |
| ALERT-004 | High | Privileged account creation carries the highest potential impact if unauthorized | Escalate/Investigate |
| ALERT-005 | Low | Security control functioned correctly; worth a passing check, not full investigation | Review |
| ALERT-006 | Medium | "Suspicious domain" is unconfirmed; requires threat intel enrichment before conclusions | Investigate |

## Prioritization Reasoning
ALERT-004 is prioritized above ALERT-002 despite ALERT-002 having more
individual events, because ALERT-004 describes a completed privileged
action rather than an in-progress attempt. Impact potential is weighted
above event count.
