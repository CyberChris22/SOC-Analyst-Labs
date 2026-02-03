# Lab 1: Installing the Wazuh Agent on Windows Endpoint and Basic Monitoring

Lab 1 focuses on installing the Wazuh agent on a Windows VM, verifying the agent is active, and confirming that basic security events—specifically failed login attempts—are successfully collected and viewable in the Wazuh dashboard. This lab establishes the foundation for later labs involving threat detection, brute-force simulation, and malware analysis.

## Objectives
- Install and verify Wazuh agent operation on a Windows endpoint.
- Confirm Sysmon is running and contributing event data.
- Identify and analyze failed login events (Event ID 4625).
- Validate Wazuh’s event collection by comparing with Windows Event Viewer.

## Environment
- Windows 10 VM (DESKTOP-MHRV979) monitored by Wazuh agent (`wazuhsvc`).
- Wazuh Manager (Ubuntu server).
- Wazuh web interface with Explore, Discover, and Threat Hunting tabs.
- Sysmon already installed from previous labs (5, 6, and 7).

## Steps Completed

1. **Verify Wazuh Agent Installation**
   - Opened Windows Services Manager (`services.msc`).
   - Confirmed the service `wazuhsvc` was running.
   - ![Wazuh agent service running](screenshots/Lab1-01_agent-service.png)
   - *Notes:* Verifies successful installation and local service operation.

2. **Verify Agent Status in Wazuh Dashboard**
   - Logged into Wazuh → Agents.
   - Confirmed the Windows endpoint (`DESKTOP-MHRV979`, agent ID 001, IP 192.168.0.216) was active and connected.
   - ![Wazuh agent status](screenshots/Lab1-02_agent-status.png)
   - *Notes:* Confirms the agent is communicating with the Wazuh manager.

3. **Identify Failed Login Events (Event ID 4625)**
   - Navigated to Discover in the Wazuh dashboard.
   - Applied filters:
     - `agent.name` = DESKTOP-MHRV979
     - `data.win.system.eventID` = 4625
   - Observed ~5 failed login events captured by Wazuh.
   - Expanded events to examine:
     - `targetUserName`
     - `logonType`
     - `failureReason`
     - `status` and `subStatus` codes
   - ![Failed login events in Wazuh](screenshots/Lab1-03_wazuh_failed_logins.png)
   - *Notes:* Confirms successful Windows event ingestion through Wazuh + Sysmon.

4. **Compare Wazuh Events with Windows Event Viewer**
   - Opened Windows Security logs in Event Viewer.
   - Located matching Event ID 4625 entries.
   - Verified timestamps, usernames, and failure codes align with Wazuh dashboard events.
   - ![Windows Event Viewer logs](screenshots/Lab1-04_windows-logs.png)
   - *Notes:* Confirms Wazuh accurately mirrors native Windows security logs.

## Key Observations
- Wazuh agent installation and connectivity were successful on first attempt.
- Sysmon + Wazuh integration correctly captured Windows failed login attempts.
- Wazuh event fields match Windows Event Viewer details, confirming reliable data ingestion.
- No dashboards, visualizations, exports, or widgets were required for Lab 1.



