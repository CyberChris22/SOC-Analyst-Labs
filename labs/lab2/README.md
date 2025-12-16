
# Lab 2: Configuring Custom Alerts and Dashboards in Wazuh

## Objective
The purpose of this lab is to create custom Wazuh rules, generate alerts from system logs, and visualize those alerts in the Wazuh Dashboard. This lab covers both Linux and Windows environments and demonstrates end-to-end verification of custom rules.

## Lab Steps and Documentation

### 1. Create Test Files for FIM Alerts
- Created custom files for Wazuh File Integrity Monitoring (FIM) testing.
- Linux test file: `C_WazuhTest_test.txt`
- Windows test file: `C_WazuhTest_test.txt`
- Screenshots:
  - `Lab2-00-Wazuh_FIM_CustomAlert_C_WazuhTest_test_txt`
  - `Lab2-01-Windows_FIM_TestFile_C_WazuhTest_test_txt`

### 2. Verify FIM Alerts in Wazuh Dashboard
- Checked that Wazuh detected changes in the FIM test files.
- Screenshots:
  - `Lab2-02-WazuhDashboard_FIM_C_WazuhTest_test_txt`
  - `Lab2-03-WazuhDashboard_ThreatHunting_C_WazuhTest_test_txt`

### 3. Generate Alerts from System Logs
- Triggered alerts using system activity and custom test logs.
- Linux alerts:
  - `Lab2-04-Ubuntu_Alerts_Log_92910_OneDrive_Explorer`
  - `Lab2-07-Ubuntu_Wazuh_Alerts_Lab2_TestFile_txt`
- Windows alerts:
  - `Lab2-05-Wazuh_Dashboard_Alert_92910_OneDrive_Explorer`
  - `Lab2-06-Windows_FIM_TestFile_C_WazuhTest_Lab2_TestFile_txt`

### 4. Create Custom Wazuh Rules
- Created custom XML rules:
```xml
<group name="custom_lab2_rules">
  <rule id="100100" level="10">
    <match>CUSTOM_LAB2_TEST</match>
    <description>Lab 2 - Custom alert triggered by CUSTOM_LAB2_TEST</description>
  </rule>

  <rule id="100101" level="8">
    <match>CUSTOM_LAB2_TEST2</match>
    <description>Lab 2 - Custom alert triggered by CUSTOM_LAB2_TEST2</description>
  </rule>
</group>
```
- Verified rules with `wazuh-logtest`.
- Screenshot: `Lab2-11-Wazuh_logtest_100101`

### 5. Verify Custom Alerts in Wazuh Dashboard
- Confirmed custom alerts appear in the Dashboard:
  - Discover view for rule 100101: `Lab2-08-Discover_rule_100101`
  - Rule definition in Management → Rules: `Lab2-09-Rule_definition_100101`

### 6. Verify Alerts in Ubuntu Terminal
- Used `tail` and `grep` to confirm custom alerts are logged in `alerts.json`.
- Screenshot: `Lab2-10-Alerts_terminal_100101`

## Summary
- Custom rules `100100` and `100101` were successfully created and tested.
- Alerts were generated and verified in both Linux and Windows environments.
- Dashboard visualizations confirmed proper integration of custom rules.
- All objectives for Lab 2 have been completed and documented.

## Screenshots
| Screenshot # | Description |
|--------------|-------------|
| Lab2-00 | Wazuh FIM alert for Linux test file `C_WazuhTest_test.txt` |
| Lab2-01 | Wazuh FIM alert for Windows test file `C_WazuhTest_test.txt` |
| Lab2-02 | Dashboard view of FIM alert for Linux test file |
| Lab2-03 | Threat Hunting view showing FIM alert activity |
| Lab2-04 | Ubuntu alerts log for OneDrive Explorer activity |
| Lab2-05 | Wazuh Dashboard alert for Windows OneDrive Explorer |
| Lab2-06 | Windows FIM test file alert confirmation |
| Lab2-07 | Ubuntu Wazuh alert for Lab2 test file |
| Lab2-08 | Dashboard Discover view for custom rule 100101 |
| Lab2-09 | Custom rule 100101 definition in Wazuh Management → Rules |
| Lab2-10 | Terminal view showing alert for 100101 in `alerts.json` |
| Lab2-11 | `wazuh-logtest` confirming rule 100101 fires correctly |




