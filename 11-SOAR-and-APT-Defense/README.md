# SOAR Automation and APT Defense

## Overview
This project demonstrates a Junior SOC Analyst's approach to security automation and Advanced Persistent Threat (APT) investigation, using simulated security events representing a potential multi-stage intrusion into TechCrush Financial Services.

## Full Report
See [reports/INC-2026-015.md](./reports/INC-2026-015.md) for the complete investigation, and [playbooks/](./playbooks/) for the automation workflow design.

## Scenario
A suspicious authentication was detected involving WIN10-01, followed by persistence, discovery, lateral movement, and a large outbound connection - six distinct events across a 30-minute window, correlated into a single potential intrusion.

## Key Finding
No individual event in this sequence was independently conclusive. The assessment rests on correlating six event types into a recognized attacker progression (initial access → persistence → discovery → lateral movement → possible exfiltration), matching the APT lifecycle model rather than any single alert.

## Automation Design
A SOAR playbook was developed to automate repetitive enrichment and investigation tasks (IP reputation, SIEM search, endpoint checks) while requiring human approval before any disruptive containment action (account disablement, host isolation).

## Severity vs. Confidence
Severity: High (based on potential business impact). Confidence: Medium-High (based on behavioral correlation, not yet definitive proof). This distinction is documented explicitly in the incident report rather than treated as one combined rating.

## Skills Demonstrated
SOAR/automation design, APT lifecycle analysis, event correlation, attack-chain mapping, incident severity vs. confidence assessment, professional incident documentation.

## Tools Used
- Bash (Ubuntu)
- grep

## Files
- `alerts/` - simulated APT alert
- `evidence/` - timeline, attack-chain analysis, IOC list
- `playbooks/` - SOAR playbook and automation decision tree
- `reports/` - full incident investigation report
