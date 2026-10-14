# Incident Response Playbook: Phishing Attack

## Scenario

TechCrush Group 24 offers cloud services to businesses in Lagos. A Cloud Operations employee receives an email that looks like it's from the company's cloud administration: "URGENT: Your cloud administrator account needs verification. Failure to verify within 24 hours will result in temporary suspension of your account." The employee clicks the link, is taken to a fake login page resembling the real cloud portal, and submits their username and password. The credentials are intercepted. Shortly after, the SOC sees a login to the employee's cloud account from an unknown location/device, and the attacker attempts to access cloud resources using the stolen credentials.

## Incident Triggers

* An urgent account-verification email
* A SOC alert showing an unusual login from an unknown device/location
* Employee credentials submitted to the fake login page
* Attempts to access cloud resources using the compromised credentials

## Playbook

|Section|Content|
|-|-|
|**Identification**|Cloud employee receives a threatening, urgent email purporting to be from the organization's cloud administration; unexpected login/authentication from an unusual location and device; unusual attempt to access cloud resources|
|**Detection and Analysis**|SOC reviews the suspicious email; identifies the sender and domain; checks whether other employees received the same email; reviews authentication logs for suspicious logins from unknown devices/locations; identifies which cloud environments/resources the attacker accessed|
|**Containment**|Temporarily disable all compromised accounts; isolate and terminate active sessions on infected systems; block malicious IP addresses and network traffic; restrict affected network segments; watch the cloud environment for further suspicious activity|
|**Eradication**|Remove all malware/malicious files using EDR and antivirus; remove unauthorized accounts; reset compromised credentials and passwords; terminate all persistence mechanisms; patch exploited vulnerabilities; check the employee's device and cloud permissions for remaining signs of compromise|
|**Recovery**|Restore the employee's cloud account after confirming it is secure; reset the password to a stronger one; re-enable appropriate access; monitor the account closely; review cloud activity and recover any lost/encrypted files; confirm no unauthorized changes remain; update security controls and hold a lessons-learned meeting|
|**Roles**|Incident Commander coordinates response and key decisions. SOC Analyst detects, escalates, and investigates (alerts, logs, email, evidence). Technical Lead handles system restoration, remediation, eradication, and troubleshooting. Communications Lead manages internal and external communication with stakeholders.|
|**Communication Plan**|SOC Analyst is notified first, documents findings, and passes information to the Incident Commander, who interacts with the affected employee for full details and notifies management. IT/Security is notified to contain the damage. The Communications Lead delivers the final incident summary and lessons learned to stakeholders and management.|
|**Metrics**|Mean Time to Detect (MTTD): how long to identify the incident. Mean Time to Respond (MTTR): how long to begin an appropriate response. Mean Time to Contain: how long to stop the incident spreading or causing more damage. Recovery Time: how long to restore affected services. Number of Incidents: count over a defined period.|



