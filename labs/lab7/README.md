# Lab 7: Reporting and Dashboard Optimization

## Objective
Create and customize dashboards and reports in Wazuh for monitoring a Windows VM. Apply filters, save views, create visualizations/widgets, and generate reports for documentation, even in a low- or no-event environment.

## Environment
- **Windows 10 VM:** DESKTOP-MHRV979 monitored by Wazuh agent (`wazuhsvc`)
- **Wazuh Manager:** Ubuntu server
- **Wazuh web interface:** Explore, Dashboard, Visualize, Discover tabs

## Lab Steps and Documentation

### 1. Verify Wazuh Agent
- Confirmed Wazuh agent running as `wazuhsvc` in Windows Services Manager
- **Screenshot:** `lab7-00_agent_status_windows.png`
- Notes: Agent connectivity to Wazuh manager verified; service running normally

### 2. Saved Filtered View in Discover
- Added filters in Discover for:
  - `agent.name` → DESKTOP-MHRV979  
  - `data.win.system.eventID` → 4720, 4728 (others not available)  
  - Optional: `rule.level` → moderate+ (adjusted using available operators)
- Saved the filtered view as **Lab7_Filters**
- **Screenshot:** `lab7-01_Discover_Filters.png`
- Notes: Filters persisted only in Discover; Threat Hunting does not retain filters

### 3. Applied Same Filters in Threat Hunting
- Mirrored filters from Discover to Threat Hunting
- **Screenshot:** `lab7-02_WazuhDashboard_FilteredView.png`
- Notes: No events were present; dashboard shows normal state despite applied filters

### 4. Exported Filtered Data
- In Discover → Reporting → Generate CSV
- Exported CSV file of filtered events as **lab7-03_Discover_FilteredExport.csv**
- Observations: CSV is empty (1 KB) due to no matching events
- Notes: Demonstrates ability to export filtered views even in low-event environments

### 5. Created Dashboard Widgets / Visualizations
- Created 3 widgets on **Lab7_CustomDashboard** using saved Lab7_Filters view:
  1. **Event ID Trends**
     - Type: Vertical Bar
     - Data source: Lab7_Filters
     - Metric: Count of events
     - X-axis: `data.win.system.eventID`
  2. **Top Event Sources**
     - Type: Vertical Bar
     - Data source: Lab7_Filters
     - Metric: Count of events
     - X-axis: `agent.name`
  3. **Event Severity Breakdown**
     - Type: Donut
     - Data source: Lab7_Filters
     - Metric: Count of events
     - X-axis: `rule.level`
- **Screenshot:** `lab7-04_CustomDashboard_Widgets.png`
- Notes: Widgets created successfully even with no events

### 6. Dashboard Overview
- Opened **Lab7_CustomDashboard** to display all 3 widgets together
- **Screenshot:** `lab7-05_CustomDashboard_Report.png`
- Notes: Dashboard layout and visualization configuration confirmed; empty counts demonstrate proper setup

## Key Observations
- Wazuh filters and visualizations function even with zero matching events
- Saved Discover views allow persistent filtering for reporting
- Threat Hunting tab does not persist filters between sessions
- Dashboard widgets can be configured from saved Discover views
- CSV exports capture filtered data for documentation, even if empty
- Custom dashboard layout preserved all created widgets

## References
- Wazuh Documentation: [https://documentation.wazuh.com/current/](https://documentation.wazuh.com/current/)
- Wazuh Dashboard and Visualizations: [https://documentation.wazuh.com/current/user-manual/kibana/index.html](https://documentation.wazuh.com/current/user-manual/kibana/index.html)
- Microsoft Event IDs: [https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4720](https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4720)

## Screenshots
- `lab7-00_agent_status_windows.png`
- `lab7-01_Discover_Filters.png`
- `lab7-02_WazuhDashboard_FilteredView.png`
- `lab7-03_Discover_FilteredExport.csv`
- `lab7-04_CustomDashboard_Widgets.png`
- `lab7-05_CustomDashboard_Report.pdf`




