# Lab 3: Valid Accounts (T1078) + File Integrity Monitoring (FIM)

## Objectives
- Detect privileged account logon abuse (**MITRE T1078**).
- Trigger and verify File Integrity Monitoring (FIM) alerts.
- Demonstrate real-time SIEM correlation and alert validation.

## Prerequisites
- Wazuh server (Amazon Linux) at https://192.168.0.73.
- Windows 10 VM with Wazuh agent (`DESKTOP-09QTA75`) installed and active.
- FIM monitoring enabled on `C:\WazuhTest`.

## Steps
1. Created test file `malicious.exe` in `C:\WazuhTest` to trigger FIM.
2. Executed `Start-Process cmd.exe -Verb runAs` to force UAC elevation and generate privileged logon events.
3. Monitored alerts in Wazuh dashboard under **Security Events**.

## Outcomes
- **FIM Alert (Rule 554):** File `malicious.exe` added at ~19:36:xx.
- **T1078 Alert (Rule 60118):** Double privileged logon detected at 19:37:16.538 (x2).
- **MITRE Mapping:** T1078 – *Valid Accounts* (Initial Access, Privilege Escalation, Persistence, Defense Evasion).

## Screenshots
- [FIM Alert 1](./assets/lab3-fim-alert1.png)
- [FIM Alert 2](./assets/lab3-fim-alert2.png)
- [T1078 Double Alert 1](./assets/lab3-T1078-Double-Alert1.png)
- [T1078 Double Alert 2](./assets/lab3-T1078-Double-Alert2.png)

## Skills Demonstrated
- MITRE ATT&CK technique simulation and detection
- Windows Event ID 4624 analysis
- FIM configuration and alert validation
- SIEM triage and correlation
