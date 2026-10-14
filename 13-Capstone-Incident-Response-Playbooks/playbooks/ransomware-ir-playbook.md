# Incident Response Playbook: Ransomware Attack

## Incident Triggers
- Administrative login/control takeover: account lockouts, unauthorized password changes
- Change in system appearance/settings: unfamiliar folders, files with strange extensions (e.g. `.lock` or alphanumeric strings), changed wallpaper
- A ransom note (usually a `.txt` file) containing the attacker's demands
- Severe system slowdown, sometimes to the point of being unusable

## Playbook

| Section | Content |
|---|---|
| **Identification** | Recognize the symptom set above (account takeover signs, file/extension changes, ransom note, severe slowdown) as consistent with a ransomware event |
| **Detection** | SIEM logs record every file change and action taken during the attack — review for the number of file modifications and logins from unusual locations. EDR alerts on mass file-renaming activity. Users report to the helpdesk that they can't open documents or see unfamiliar file names/extensions. |
| **Containment** | Immediately isolate the affected system from the network. Disable affected user accounts. Block suspected IP addresses. Quarantine unaffected systems and check them for signs of compromise. **Do not shut the system down** — this destroys forensic evidence. Isolate backup systems from the network so they cannot be encrypted too. Take forensic images/memory captures where appropriate. Run full network diagnostics to confirm the rest of the network is risk-free. |
| **Eradication** | Search SIEM/EDR logs for indicators of compromise (IOCs). Document and preserve evidence (method of compromise, systems affected). Identify and remove the attack vector (unpatched software, weak passwords, phishing email) to prevent recurrence. Identify and remove attacker persistence (unauthorized admin accounts, PowerShell profiles, remote management tools). Quarantine and kill the ransomware process using antivirus/EDR. Remove the ransomware. Reset compromised credentials (user and admin). Scan to verify the system is ransomware-free; patch or do a clean OS reinstall if needed. Confirm the system is clean. |
| **Recovery** | Identify and verify clean backups (pre-attack backups are usually malware-free, but still scan to confirm). Restore data from the verified clean backup (user profiles, application data, documents, configuration). Test each restored system and confirm security controls before reconnecting it to the network. Reconnect systems to production gradually, one at a time, with testing at each step. Monitor restored systems for unusual foreground/background process activity. |
| **Roles** | Identification: SOC Analyst (Tier 1). Detection: SOC Analyst. Containment: Incident Response team. Eradication: IR team + Technical Lead. Recovery: IT / Communications Lead / Recovery Team. |
| **Communication Plan** | Tier 1 SOC Analyst identifies a suspected attack from SIEM logs, documents findings, and refers to Tier 2 for further analysis. Tier 2 confirms the ransomware attack and transfers all relevant logs, detection time, affected computers, and user accounts to the Incident Response Team. The IR Team contains the spread and hands over to the Eradication Team. The Eradication Team removes malware and blocks the attack vector. The Recovery Team restores systems free of ransomware. Channels: SOC-internal — secure chat. SOC → IR — incident ticket. IR → Eradication/IT — secure chat. Eradication → Recovery — incident ticket plus formal handover. |
| **Metrics** | Detection: 0–15 minutes. Containment: 15–60 minutes. Eradication: 1–24 hours. Recovery: 24–72 hours. |

## The One Rule Worth Remembering
Do not power off a system suspected of ransomware infection. Shutting it down destroys volatile evidence held in RAM (running processes, active connections, encryption keys) that a forensic investigator needs afterward. Isolate it from the network instead — cut its ability to communicate, without erasing what it currently holds in memory.
