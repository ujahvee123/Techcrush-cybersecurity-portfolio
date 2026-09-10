# SOC Alert Triage and Incident Handling

## Project Overview
This project simulates the daily activities of a Junior SOC Analyst working within the TechCrush Financial Services security operations environment, covering alert triage, investigation, and professional incident reporting.

## Scenario
The SOC received six alerts during an overnight monitoring period. The analyst was responsible for prioritizing the alerts and investigating the most significant one: suspicious SSH authentication activity affecting the LINUX01 server.

## Full Report
See [reports/INC-2026-014.md](./reports/INC-2026-014.md) for the complete investigation.

## Key Decision
ALERT-004 (unauthorized admin account creation) was prioritized above ALERT-002 (repeated SSH failures) despite having fewer individual events, because it described a completed privileged action rather than an in-progress attack attempt. Impact potential was weighted above event count.

## Key Finding
Repeated SSH authentication failures from a single external source were followed by successful authentication using a previously-targeted account. The activity was assessed as suspicious and requiring escalation, without overstating it as confirmed compromise.

## Skills Demonstrated
SOC alert triage, prioritization reasoning, Linux log analysis, event correlation, incident severity assessment, professional incident documentation, escalation decision-making.

## Tools Used
- Ubuntu
- grep, wc, sort, uniq
