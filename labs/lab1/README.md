# Lab 1: Installing the Wazuh Agent on Windows Endpoint and Basic Monitoring

Lab 1 demonstrates installing the Wazuh agent on a Windows VM, verifying agent status, capturing failed login events, exporting data, and creating a minimal dashboard to visualize collected events, even in a low-event environment.

## Objectives
- Verify Wazuh agent installation and connectivity.
- Capture failed login events from the Windows VM.
- Apply filters in Discover to focus on relevant events.
- Export filtered events to CSV for documentation.
- Create minimal dashboard widgets to visualize failed logins.
- Understand dashboard behavior when no new events occur.

## Environment
- Windows 10 VM (DESKTOP-MHRV979) monitored by Wazuh agent (`wazuhsvc`).
- Wazuh Manager (Ubuntu server).
- Wazuh web interface with Explore, Dashboard, Visualize, and Discover tabs.

## Steps Completed

1. **Verify Wazuh Agent**
   - Confirmed Wazuh agent running as `wazuhsvc` in Windows Services Manager.
   - Screenshot: `Lab1-01_agent-service.png`
   - Notes: Verified agent connectivity to Wazuh manager, no issues with service status.

2. **Check Agent Status in Wazuh**
   - Opened Wazuh Manager dashboard and confirmed agent is active.
   - Screenshot: `Lab1-02_agent-status.png`
   - Notes: Agent name DESKTOP-MHRV979, IP 192.168.0.216.

3. **Identify Failed Login Events**
   - Opened Discover and applied filters:
     - `agent.name` → DESKTOP-MHRV979
     - `data.win.system.eventID` → 4625
   - Approximately 5–6 failed login events were identified.
   - Expanded events to view detailed fields (`targetUserName`, `logonType`, `failureReason`).
   - Screenshot: `Lab1-03_wazuh_failed_logins.png`
   - Notes: Confirmed failed login events are captured correctly by Wazuh agent.

4. **Compare with Windows Event Viewer**
   - Opened Windows Security Event Viewer to match failed login events from Wazuh.
   - Screenshot: `Lab1-04_windows-logs.png`
   - Notes: Windows logs confirm the same failed login attempts captured in Wazuh.

5. **Saved Filtered View in Discover**
   - Saved filtered view with the same parameters to persist configuration for reporting.
   - Screenshot: `Lab1-05_filtered_view.png`
   - Notes: Ensures consistent reporting and dashboard data source.

6. **Exported Filtered Data**
   - In Discover → Share → CSV Reports → Generate CSV.
   - Downloaded CSV file of filtered events as `Lab1-discover-export.csv`.
   - Screenshot: `Lab1-06_csv_export.png`
   - Observations: CSV contains all filtered failed login events from table view, not expanded events.
   - Notes: Demonstrates ability to export filtered views for documentation.

7. **Created Dashboard Widgets / Visualizations**
   - Created 3 widgets on `Lab1_CustomDashboard` using saved filtered Discover view:
     1. **Failed Logins by User**
        - Type: Vertical Bar
        - Data source: `wazuh-alerts-*`
        - Metric: Count of events
        - X-axis: `data.win.eventdata.targetUserName.keyword`
     2. **Failed Logins Over Time**
        - Type: Line Chart
        - Data source: `wazuh-alerts-*`
        - Metric: Count of events
        - X-axis: `@timestamp`
     3. **Failed Logins by Workstation**
        - Type: Donut / Pie Chart
        - Data source: `wazuh-alerts-*`
        - Metric: Count of events
        - X-axis: `data.win.eventdata.workstationName.keyword`
   - Screenshot: `Lab1-07_lab_dashboard.png`
   - Notes: Dashboard demonstrates widget configuration; no new events occurred, so counts are empty.

8. **Dashboard Overview**
   - Opened `Lab1_CustomDashboard` to display all 3 widgets together.
   - Screenshot: `Lab1-07_lab_dashboard.png`
   - Notes: Layout and visualization configuration confirmed; dashboard updates automatically with new events.

9. **Key Observations**
   - Wazuh agent correctly installed and running on Windows VM.
   - Failed login events captured and verified via Windows Event Viewer.
   - Saved Discover views allow consistent filtering for reporting.
   - CSV exports capture filtered data for documentation.
   - Dashboard widgets demonstrate visualization even with low or no events.

10. **References**
    - Wazuh Documentation: https://documentation.wazuh.com/current/
    - Wazuh Dashboard and Visualizations: https://documentation.wazuh.com/current/user-manual/kibana/index.html
    - Microsoft Event IDs: https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4625

11. **Screenshots**
    - `Lab1-01_agent_service_running.png`
    - `Lab1-02_agent_active_in_wazuh.png`
    - `Lab1-03_wazuh_failed_logins.png`
    - `Lab1-04_windows_event_viewer_failed_logins.png`
    - `Lab1-05a_discover_filtered_events.png`
    - `Lab1-05b_discover_filtered_events.png`
    - `Lab1-06_csv_export`
    - `Lab1-07_lab_dashboard.png`


