# Attack Chain Analysis

| Time | Activity | Potential APT Stage |
|---|---|---|
| 09:14 | Unusual authentication | Initial Access |
| 09:18 | Scheduled task created | Persistence |
| 09:24 | Discovery activity | Discovery |
| 09:31 | Authentication attempt against FS01 | Lateral Movement (attempt) |
| 09:35 | Successful authentication against FS01 | Lateral Movement (achieved) |
| 09:44 | Large outbound connection | Possible Exfiltration |

## Why This Mapping Matters
No single event here is conclusive on its own. The value of this
mapping is showing that the sequence follows a recognized attacker
progression rather than six unrelated events, this pattern, not any
individual line, is the actual evidence supporting escalation.
