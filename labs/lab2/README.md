# Lab 2: Threat Detection with Wazuh

## Objectives
- Detect simulated malicious activity on a Windows endpoint.
- Configure File Integrity Monitoring (FIM) for threat detection.
- Demonstrate SIEM integration and alert response.

## Prerequisites
- Wazuh server (Amazon Linux) at https://192.168.0.73.
- Windows 10 VM with Wazuh agent (`DESKTOP-09QTA75`) installed.

## Steps
1. Configured FIM to monitor `C:\WazuhTest` by editing `ossec.conf`.
2. Simulated malware by creating and deleting `malware_test.exe` in `C:\WazuhTest`.
3. Monitored alerts in Wazuh dashboard under **Threat Hunting > Events**.

## Outcomes
- Detected **“File added to the system”** at 17:06:22 CDT.
- Detected **“File deleted”** at 17:09:24 CDT.
- Screenshots:
  - [Malware Alert 1](./assets/lab2-malware-alert.png)
  - [Malware Alert 2](./assets/lab2-malware-alert2.png)

## Skills Demonstrated
- Threat detection configuration
- SIEM alert monitoring
- File integrity monitoring setup




