# Lab 7: Reporting and Dashboard Optimization

Lab 7 demonstrates creating and customizing dashboards and reports in Wazuh for monitoring a Windows VM. The lab focuses on applying filters, saving views, creating visualizations/widgets, and generating reports for documentation, even in a low- or no-event environment.

## Objectives
- Apply filters to focus on specific hosts, event types, and severities.
- Save filtered views for consistent reporting.
- Create dashboard widgets to visualize event trends and severity breakdowns.
- Export data and dashboard snapshots for documentation purposes.
- Understand limitations when no events are present.

## Environment
- Windows 10 VM (DESKTOP-MHRV979) monitored by Wazuh agent (`wazuhsvc`).
- Wazuh Manager (Ubuntu server).
- Wazuh web interface with Explore, Dashboard, Visualize, and Discover tabs.

## Steps Completed

1. **Verify Wazuh Agent**
   - Confirmed Wazuh agent running as `wazuhsvc` in Windows Services Manager.
   - Screenshot: `lab7-00_agent_status_windows.png`
   - Notes: Verified agent connectivity to Wazuh manager, no issues with service status.

2. **Saved Filtered View in Discover**
   - Added filters in Discover for:
     - `agent.name` → DESKTOP-MHRV979
     - `data.win.system.eventID` → 4720, 4728 (other IDs not available in environment)
     - Optional: `rule.level` → moderate+ (adjusted using available operators)
   - Saved the filtered view as `Lab7_Filters`.
   - Screenshot: `lab7-01_Discover_Filters.png`
   - Notes: Filters persisted only in Discover. Threat Hunting does not retain filters after leaving the page.

3. **Applied Same Filters in Threat Hunting**
   - Filters mirrored from Discover to Threat Hunting.
   - Screenshot: `lab7-02_WazuhDashboard_FilteredView.png`
   - Notes: No events were present; dashboard shows normal state even though filters were applied.

4. **Exported Filtered Data**
   - In Discover → Reporting → Generate CSV.
   - Exported CSV file of filtered events as `lab7-03_Discover_FilteredExport.csv`.
   - Observations: CSV is empty (1 KB) because no matching events exist.
   - Notes: Demonstrates ability to export filtered views even in low-event environments.

5. **Created Dashboard Widgets / Visualizations**
   - Created 3 widgets on `Lab7_CustomDashboard` using saved `Lab7_Filters` view:
     1. **Event ID Trends**
        - Type: Vertical Bar
        - Data source: `Lab7_Filters`
        - Metric: Count of events
        - X-axis: `data.win.system.eventID`
     2. **Top Event Sources**
        - Type: Vertical Bar
        - Data source: `Lab7_Filters`
        - Metric: Count of events
        - X-axis: `agent.name`
     3. **Event Severity Breakdown**
        - Type: Donut
        - Data source: `Lab7_Filters`
        - Metric: Count of events
        - X-axis: `rule.level`
   - Screenshot: `lab7-04_CustomDashboard_Widgets.png`
   - Notes: All widgets created successfully, even though there are no events.

6. **Dashboard Overview**
   - Opened `Lab7_CustomDashboard` to display all 3 widgets together.
   - Screenshot: `lab7-05_CustomDashboard_Report.png`
   - Notes: Dashboard shows widgets with empty counts, demonstrating layout and visualization configuration.

7. **Key Observations**
   - Wazuh filters and visualizations work even with zero matching events.
   - Saved Discover views allow persistent filtering for reporting.
   - Threat Hunting tab does not persist filters between sessions.
   - Dashboard widgets can be configured from saved Discover views.
   - CSV exports capture filtered data for documentation, even if empty.
   - Custom dashboard layout preserved all created widgets.

8. **References**
   - Wazuh Documentation: https://documentation.wazuh.com/current/
   - Wazuh Dashboard and Visualizations: https://documentation.wazuh.com/current/user-manual/kibana/index.html
   - Microsoft Event IDs: https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4720

9. **Screenshots**
   - `lab7-00_agent_status_windows.png`
   - `lab7-01_Discover_Filters.png`
   - `lab7-02_WazuhDashboard_FilteredView.png`
   - `lab7-03_Discover_FilteredExport.csv`
   - `lab7-04_CustomDashboard_Widgets.png`
   - `lab7-05_CustomDashboard_Report.png`




