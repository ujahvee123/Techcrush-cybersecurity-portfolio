# Proactive Threat Hunting: Credential-Guessing Activity Against LINUX01

## Project Overview
A proactive threat hunt performed in the TechCrush Financial Services simulated SOC environment, testing a hypothesis about credential-guessing behavior across two external source IPs and distinguishing targeted attack risk from automated scanning noise.

## Full Report
See [reports/threat-hunting-report.md](./reports/threat-hunting-report.md) for the complete investigation, including methodology, findings, and detection recommendations.

## Hunting Hypothesis
Multiple external sources may be conducting credential-guessing attacks against LINUX01, and their behavior may differ enough to distinguish targeted attacks from automated/opportunistic scanning.

## Key Findings
- **203.0.113.50 (Medium-High risk):** 4 failed attempts across 3 accounts, followed by a successful login on a valid, previously-targeted account.
- **198.51.100.77 (Low risk):** 3 failed attempts, all against nonexistent accounts, no success — consistent with automated scanning.

The key distinguishing factor whether targeted usernames were valid accounts and whether authentication succeeded.

## Skills Demonstrated
Threat hunting methodology, hypothesis development and testing, Linux log analysis, comparative risk assessment, detection engineering fundamentals.

## Tools Used
- Ubuntu

## Files
- `evidence/` — raw authentication log and event timeline
- `notes/` — hunting hypothesis
- `detections/` — proposed detection logic
- `reports/` — full threat hunting report
