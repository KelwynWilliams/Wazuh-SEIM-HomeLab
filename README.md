# Wazuh SIEM Home Lab

![Wazuh_Dashboard](screenshots/Wazuh.png)

## Overview
Deployed a Wazuh SIEM in a VMware Workstation virtualized environment 
to monitor a Windows 10 endpoint. Simulated five real-world attack 
techniques and investigated resulting alerts mapped to the MITRE 
ATT&CK framework. Documented all findings in a formal incident 
response report.

## Tools & Technologies
- VMware Workstation Pro 17
- Wazuh SIEM 4.7
- Ubuntu Server 22.04 LTS
- Windows 10 Pro

## Lab Architecture
[Wazuh Manager] ←→ [Windows 10 Endpoint]
Ubuntu Server 22.04       Windows 10 Pro
Wazuh 4.7                 Wazuh Agent 4.7
10.0.0.242               10.0.0.235

## Attacks Simulated & Detected

| # | Attack | MITRE ID | Tactic | Event ID |
|---|--------|----------|--------|----------|
| 1 | Brute Force Login | T1110 | Credential Access | 4625 |
| 2 | File Integrity Violation | T1070.004 | Defense Evasion | — |
| 3 | New Admin Account | T1098, T1484 | Persistence | 4720, 4732 |
| 4 | Clear Event Logs | T1070 | Defense Evasion | 104 |
| 5 | Malicious Service Creation | T1543.003 | Persistence | 7045 |

## Key Skills Demonstrated
- SIEM deployment and configuration from scratch
- Windows endpoint agent deployment and tuning
- File Integrity Monitoring (FIM) configuration
- Windows Event Log analysis
- MITRE ATT&CK framework mapping
- Detection tuning and gap analysis
- Incident documentation and reporting

## Detection Highlights

### Brute Force — T1110
##### Brute Force Alert
![Brute Force Alert](screenshots/1-brute-force-alert.png)
##### Brute Force Detail
![Brute Force Detail](screenshots/1-brute-force-detail.png)
##### Brute Force MITRE
![Brute Force MITRE](screenshots/1-brute-force-mitre.png)

### File Integrity Violation — T1070.004
##### FIM File Added Alert
![FIM Alert](screenshots/2-file-integrity-addition-alert.png)
##### FIM File Added Detail
![FIM Detail](screenshots/2-file-integrity-addition-detail.png)
##### FIM File Deleted Alert
![FIM Alert](screenshots/2-file-integrity-deletion-alert.png)
##### FIM File Deleted Detail
![FIM Detail](screenshots/2-file-integrity-deletion-detail.png)
##### FIM File Deleted MITRE
![FIM MITRE](screenshots/2-file-integrity-deletion-mitre.png)

### New Admin Account — T1098, T1484
##### Admin Acct Creation Alert
![Admin Alert](screenshots/3-admin-account-creation-alert.png)
##### Admin Acct Creation Detail
![Admin Detail](screenshots/3-admin-account-creation-detail-1.png)
![Admin Detail](screenshots/3-admin-account-creation-detail-2.png)
##### Admin Acct Creation MITRE
![Admin MITRE](screenshots/3-admin-account-creation-mitre.png)
##### Admin Acct Localgroup Alert
![Admin Alert](screenshots/3-admin-account-localgroup-alert.png)
##### Admin Acct Localgroup Detail
![Admin Detail](screenshots/3-admin-account-localgroup-detail-1.png)
![Admin Detail](screenshots/3-admin-account-localgroup-detail-2.png)
##### Admin Acct Localgroup MITRE
![Admin MITRE](screenshots/3-admin-account-localgroup-mitre.png)

### Clear Event Logs — T1070.001
##### Event Log Alert
![Event Log Alert](screenshots/4-event-log-clear-alert.png)
##### Event Log Detail
![Event Log Detail](screenshots/4-event-log-clear-detail.png)
##### Event Log MITRE
![Event Log MITRE](screenshots/4-event-log-clear-mitre.png)

### Malicious Service Creation — T1543.003
##### Service Alert
![Service Alert](screenshots/5-service-creation-alert.png)
##### Service Detail
![Service Detail](screenshots/5-service-creation-detail.png)
##### Service MITRE
![Service MITRE](screenshots/5-service-creation-mitre.png)

## Detection Gaps & Tuning
During this exercise several configurations required manual tuning:

- **FIM** required adding System32 to ossec.conf with realtime enabled
- **Registry monitoring** required explicit windows_registry entries
- **PowerShell logging** required enabling Script Block Logging via registry

This reflects real SOC work where continuous detection tuning is as 
important as initial SIEM deployment.

## Incident Report
Full findings documented in [incident-report.pdf](incident-report.pdf)
```
