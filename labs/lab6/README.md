\# Lab 6: Incident Response Simulation



Lab 6 demonstrates a simulated incident response workflow on a Windows 10 VM monitored by Wazuh. The lab focuses on generating suspicious events, detecting them via Sysmon and Wazuh, performing containment and evidence collection, simulating recovery, and documenting findings. This lab simulates threat scenarios in a safe environment without deploying real malware.



Objectives: Generate simulated security events, detect suspicious activity using Sysmon and Wazuh, practice containment and evidence collection, understand event correlation and monitoring limitations, and document incident response actions.



Environment: Windows 10 VM (target system), Wazuh agent running as `wazuhsvc`, Ubuntu server running Wazuh manager, Event Viewer for Sysmon, Security, System, and Application logs.



\## Steps Completed



1\. \*\*Verify Wazuh Agent\*\*

&nbsp;  - Confirmed Wazuh agent running as `wazuhsvc` in Windows Services Manager.

&nbsp;  - Screenshot: lab6-00\_agent\_status\_windows.png

&nbsp;  - Notes: Verified agent connectivity to Wazuh manager, no issues with service status.



2\. \*\*Generate Test Events\*\*

&nbsp;  - Created a test user account and added to Administrators group to simulate account compromise.

&nbsp;  - Event Viewer captured:

&nbsp;    - User Account Creation: Event ID 4720

&nbsp;    - Admin Group Membership Change: Event ID 4728

&nbsp;  - Wazuh alert triggered for admin group change.

&nbsp;  - Screenshots: lab6-01\_UserAccountCreated\_4720.png, lab6-02\_AdminGroupChange\_4728.png, lab6-03\_WazuhAlert\_AdminGroupChange.png

&nbsp;  - Notes: Wazuh alerted on admin group changes but did not alert on user creation alone.



3\. \*\*Powershell EncodedCommand Event\*\*

&nbsp;  - Executed `powershell.exe -EncodedCommand` to simulate suspicious activity.

&nbsp;  - Sysmon captured process creation (Event ID 1) and file creation events (Event ID 11).

&nbsp;  - Screenshots: lab6-04\_Sysmon\_Powershell\_encoded.png, lab6-06\_Sysmon\_Powershell\_Encoded.png

&nbsp;  - Notes: Wazuh did not trigger an alert for EncodedCommand; Event Viewer showed both process creation and file creation.



4\. \*\*LabIR Marker Event\*\*

&nbsp;  - Generated LabIR Marker event in Sysmon and Application logs.

&nbsp;  - Screenshots: lab6-07\_FileCreate\_sysmon.png, lab6-08\_LabIR\_Marker\_Event.png

&nbsp;  - Notes: Event captured in Event Viewer. Wazuh did not trigger alert. Used for safe simulation of incident marker.



5\. \*\*DNS Lookup Simulation (Timeouts)\*\*

&nbsp;  - Simulated DNS lookup failure to test network monitoring.

&nbsp;  - Sysmon Event ID captured: 600 (DNS query timeout)

&nbsp;  - Screenshot: lab6-05\_Simulated\_DNS\_Timeout\_600.png

&nbsp;  - Notes: Event captured in Event Viewer. Wazuh did not trigger alert. Attempted other Event IDs (6118 / 1014), but they did not appear. Observed filtering and viewing issues: Event Viewer limited some ID ranges; confirmed using Sysmon logs.



6\. \*\*Containment and Evidence Collection\*\*

&nbsp;  - \*\*6.A Process Containment\*\*

&nbsp;    - Identified suspicious PowerShell process.

&nbsp;    - Terminated using: `Get-Process -Name powershell | Stop-Process -Force`

&nbsp;    - Screenshots:

&nbsp;      - lab6-09\_Containment\_TaskManager.png (Task Manager showing stopped process)

&nbsp;      - lab6-09\_ProcessList\_Evidence.png (Process list exported for evidence)

&nbsp;    - Evidence file created: C:\\process\_list.txt

&nbsp;    - Notes: Safely terminated process, exported evidence.

&nbsp;  - \*\*6.B Network Containment\*\*

&nbsp;    - Disabled VM network adapter to simulate isolation: `Disable-NetAdapter -Name "Ethernet" -Confirm:$false`

&nbsp;    - Screenshot: lab6-10\_Containment\_NetworkDisabled.png

&nbsp;    - System log captured Event ID 10016 (network adapter status event), did not capture Event IDs 27/32/4201 as expected.

&nbsp;  - \*\*6.C Service Restoration\*\*

&nbsp;    - Restarted Wazuh agent (`wazuhsvc`) to resume monitoring.

&nbsp;    - Screenshot: lab6-12\_Wazuh\_Service\_Restored.png



7\. \*\*Evidence Collection Commands\*\*

&nbsp;  - Sysmon events: `wevtutil qe Microsoft-Windows-Sysmon/Operational /f:text /c:50 > C:\\Lab6\_Sysmon\_Events.txt`

&nbsp;  - Security events: `wevtutil qe Security /f:text /c:50 > C:\\Lab6\_Security\_Events.txt`

&nbsp;  - Notes: Captured last 50 events for both logs, retained as evidence for incident reporting.



8\. \*\*Observed Event IDs and Notes\*\*

&nbsp;  - User account creation: 4720

&nbsp;  - Admin group change: 4728

&nbsp;  - Powershell EncodedCommand: Sysmon 1 (process creation) \& 11 (file creation)

&nbsp;  - LabIR Marker: Sysmon 11, Application 11

&nbsp;  - DNS timeout: Sysmon 600

&nbsp;  - Network adapter disabled: 10016 (System)

&nbsp;  - Notes:

&nbsp;    - Wazuh triggered only on admin group change (4728).

&nbsp;    - Sysmon provided full visibility for EncodedCommand, LabIR Marker, and DNS timeout.

&nbsp;    - Event Viewer filtering limitations required adjustments to ID ranges and query methods.

&nbsp;    - Powershell queries needed removal of `-First` to execute correctly; long execution times observed.

&nbsp;    - Multiple screenshot capture points documented for correlation.



9\. \*\*Key Lessons Learned\*\*

&nbsp;  - Wazuh relies on pre-configured rules; not all suspicious activity triggers alerts.

&nbsp;  - Sysmon is critical for granular visibility into processes, file creations, registry, and network activity.

&nbsp;  - Safe containment simulations can include stopping processes and disabling network adapters.

&nbsp;  - Evidence collection should include logs, process lists, and screenshots.

&nbsp;  - LabIR Marker events are useful for simulating real incidents safely.

&nbsp;  - DNS/Network simulations may not always trigger alerts depending on configuration and OS limitations.



10\. \*\*References\*\*

&nbsp;   - Sysmon Documentation: https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon

&nbsp;   - Wazuh Documentation: https://documentation.wazuh.com/current/

&nbsp;   - Microsoft Event IDs: https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4720



11\. \*\*Screenshots\*\*

&nbsp;   - lab6-00\_agent\_status\_windows.png

&nbsp;   - lab6-01\_UserAccountCreated\_4720.png

&nbsp;   - lab6-02\_AdminGroupChange\_4728.png

&nbsp;   - lab6-03\_WazuhAlert\_AdminGroupChange.png

&nbsp;   - lab6-04\_Sysmon\_Powershell\_encoded.png

&nbsp;   - lab6-05\_Simulated\_DNS\_Timeout\_600.png

&nbsp;   - lab6-06\_Sysmon\_Powershell\_Encoded.png

&nbsp;   - lab6-07\_FileCreate\_sysmon.png

&nbsp;   - lab6-08\_LabIR\_Marker\_Event.png

&nbsp;   - lab6-09\_Containment\_TaskManager.png

&nbsp;   - lab6-09\_ProcessList\_Evidence.png

&nbsp;   - lab6-10\_Containment\_NetworkDisabled.png

&nbsp;   - lab6-12\_Wazuh\_Service\_Restored.png



