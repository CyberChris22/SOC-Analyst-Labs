# Lab 6: Incident Response Simulation

Lab 6 demonstrates a simulated incident response workflow on a Windows 10 VM monitored by Wazuh. The lab focuses on generating suspicious events, detecting them via Sysmon and Wazuh, performing containment and evidence collection, simulating recovery, and documenting findings. This lab simulates threat scenarios in a safe environment without deploying real malware.

**Objectives:** Generate simulated security events, detect suspicious activity using Sysmon and Wazuh, practice containment and evidence collection, understand event correlation and monitoring limitations, and document incident response actions.

**Environment:** Windows 10 VM (target system), Wazuh agent running as `wazuhsvc`, Ubuntu server running Wazuh manager, Event Viewer for Sysmon, Security, System, and Application logs.

---

## Steps Completed

### 1. Verify Wazuh Agent
- Confirmed Wazuh agent running as `wazuhsvc` in Windows Services Manager.
- Screenshot: `lab6-00_agent_status_windows.png`
- Notes: Verified agent connectivity to Wazuh manager, no issues with service status.

### 2. Generate Test Events
- Created a test user account and added to Administrators group to simulate account compromise.
- Event Viewer captured:
  - User Account Creation: Event ID 4720
  - Admin Group Membership Change: Event ID 4728
- Wazuh alert triggered for admin group change.
- Screenshots: `lab6-01_UserAccountCreated_4720.png`, `lab6-02_AdminGroupChange_4728.png`, `lab6-03_WazuhAlert_AdminGroupChange.png`
- Notes: Wazuh alerted on admin group changes but did not alert on user creation alone.

### 3. Powershell EncodedCommand Event
- Executed `powershell.exe -EncodedCommand` to simulate suspicious activity.
- Sysmon captured process creation (Event ID 1) and file creation events (Event ID 11).
- Screenshots: `lab6-04_Sysmon_Powershell_encoded.png`, `lab6-06_Sysmon_Powershell_Encoded.png`
- Notes: Wazuh did not trigger an alert for EncodedCommand; Event Viewer showed both process creation and file creation.

### 4. LabIR Marker Event
- Generated LabIR Marker event in Sysmon and Application logs.
- Screenshots: `lab6-07_FileCreate_sysmon.png`, `lab6-08_LabIR_Marker_Event.png`
- Notes: Event captured in Event Viewer. Wazuh did not trigger alert. Used for safe simulation of incident marker.

### 5. DNS Lookup Simulation (Timeouts)
- Simulated DNS lookup failure to test network monitoring.
- Sysmon Event ID captured: 600 (DNS query timeout)
- Screenshot: `lab6-05_Simulated_DNS_Timeout_600.png`
- Notes: Event captured in Event Viewer. Wazuh did not trigger alert. Attempted other Event IDs (6118 / 1014), but they did not appear. Observed filtering and viewing issues: Event Viewer limited some ID ranges; confirmed using Sysmon logs.

### 6. Containment and Evidence Collection
**6.A Process Containment**
- Identified suspicious PowerShell process.
- Terminated using: `Get-Process -Name powershell | Stop-Process -Force`
- Screenshots:
  - `lab6-09_Containment_TaskManager.png` (Task Manager showing stopped process)
  - `lab6-09_ProcessList_Evidence.png` (Process list exported for evidence)
- Evidence file created: `C:\process_list.txt`
- Notes: Safely terminated process, exported evidence.

**6.B Network Containment**
- Disabled VM network adapter to simulate isolation: `Disable-NetAdapter -Name "Ethernet" -Confirm:$false`
- Screenshot: `lab6-10_Containment_NetworkDisabled.png`
- System log captured Event ID 10016 (network adapter status event), did not capture Event IDs 27/32/4201 as expected.

**6.C Service Restoration**
- Restarted Wazuh agent (`wazuhsvc`) to resume monitoring.
- Screenshot: `lab6-12_Wazuh_Service_Restored.png`

### 7. Evidence Collection Commands
- Sysmon events: `wevtutil qe Microsoft-Windows-Sysmon/Operational /f:text /c:50 > C:\Lab6_Sysmon_Events.txt`
- Security events: `wevtutil qe Security /f:text /c:50 > C:\Lab6_Security_Events.txt`
- Notes: Captured last 50 events for both logs, retained as evidence for incident reporting.

### 8. Observed Event IDs and Notes
- User account creation: 4720
- Admin group change: 4728
- Powershell EncodedCommand: Sysmon 1 (process creation) & 11 (file creation)
- LabIR Marker: Sysmon 11, Application 11
- DNS timeout: Sysmon 600
- Network adapter disabled: 10016 (System)
- Notes:
  - Wazuh triggered only on admin group change (4728).
  - Sysmon provided full visibility for EncodedCommand, LabIR Marker, and DNS timeout.
  - Event Viewer filtering limitations required adjustments to ID ranges and query methods.
  - Powershell queries needed removal of `-First` to execute correctly; long execution times observed.
  - Multiple screenshot capture points documented for correlation.

### 9. Key Lessons Learned
- Wazuh relies on pre-configured rules; not all suspicious activity triggers alerts.
- Sysmon is critical for granular visibility into processes, file creations, registry, and network activity.
- Safe containment simulations can include stopping processes and disabling network adapters.
- Evidence collection should include logs, process lists, and screenshots.
- LabIR Marker events are useful for simulating real incidents safely.
- DNS/Network simulations may not always trigger alerts depending on configuration and OS limitations.

### 10. References
- Sysmon Documentation: https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon
- Wazuh Documentation: https://documentation.wazuh.com/current/
- Microsoft Event IDs: https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4720

### 11. Screenshots
- `lab6-00_agent_status_windows.png`
- `lab6-01_UserAccountCreated_4720.png`
- `lab6-02_AdminGroupChange_4728.png`
- `lab6-03_WazuhAlert_AdminGroupChange.png`
- `lab6-04_Sysmon_Powershell_encoded.png`
- `lab6-05_Simulated_DNS_Timeout_600.png`
- `lab6-06_Sysmon_Powershell_Encoded.png`
- `lab6-07_FileCreate_sysmon.png`
- `lab6-08_LabIR_Marker_Event.png`
- `lab6-09_Containment_TaskManager.png`
- `lab6-09_ProcessList_Evidence.png`
- `lab6-10_Containment_NetworkDisabled.png`
- `lab6-12_Wazuh_Service_Restored.png`
