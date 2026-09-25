# Threat Intelligence Analysis: Suspicious SSH Authentication

## Project Overview
A beginner-level threat intelligence investigation performed in the TechCrush Financial Services simulated SOC environment, analyzing suspicious SSH authentication activity and applying threat intelligence principles to assess risk without overstating conclusions.

## Full Report
See [reports/threat-intelligence-report.md](./reports/threat-intelligence-report.md) for the complete analysis.

## Key Finding
203.0.113.50 generated 4 failed SSH authentication attempts across 3 accounts (admin, root, alice), followed by 1 successful login to the alice account. The pattern is suspicious and warrants further investigation; the available evidence does not independently confirm compromise.

## Skills Demonstrated
Threat intelligence fundamentals, IOC identification, log analysis (grep/sort/uniq), risk assessment, cautious evidence-based reporting.

## Tools Used
- Ubuntu

