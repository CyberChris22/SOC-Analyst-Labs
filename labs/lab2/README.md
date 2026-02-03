# Lab 2: Configuring Custom Alerts and Dashboards in Wazuh

## Objective
The purpose of this lab is to create custom Wazuh rules, generate alerts from system logs, and visualize those alerts in the Wazuh Dashboard. This lab covers both Linux and Windows environments and demonstrates end-to-end verification of custom rules.

## Lab Steps and Documentation

### 1. Create Test Files for FIM Alerts
- Created custom files for Wazuh File Integrity Monitoring (FIM) testing.
- Linux test file: `C_WazuhTest_test.txt`
- Windows test file: `C_WazuhTest_test.txt`
- Screenshots:
  - ![Wazuh FIM alert for Linux test file](Assets/Lab2-00-Wazuh_FIM_CustomAlert_C_WazuhTest_test_txt.png)
  - ![Wazuh FIM alert for Windows test file](Assets/Lab2-01-Windows_FIM_TestFile_C_WazuhTest_test_txt.png)

### 2. Verify FIM Alerts in Wazuh Dashboard
- Checked that Wazuh detected changes in the FIM test files.
- Screenshots:
  - ![Dashboard view of FIM alert for Linux test file](Assets/Lab2-02-WazuhDashboard_FIM_C_WazuhTest_test_txt.png)
  - ![Threat Hunting view showing FIM alert activity](Assets/Lab2-03-WazuhDashboard_ThreatHunting_C_WazuhTest_test_txt.png)

### 3. Generate Alerts from System Logs
- Triggered alerts using system activity and custom test logs.
- Linux alerts:
  - ![Ubuntu alerts log for OneDrive Explorer activity](Assets/Lab2-04-Ubuntu_Alerts_Log_92910_OneDrive_Explorer.png)
  - ![Ubuntu Wazuh alert for Lab2 test file](Assets/Lab2-07-Ubuntu_Wazuh_Alerts_Lab2_TestFile_txt.png)
- Windows alerts:
  - ![Wazuh Dashboard alert for Windows OneDrive Explorer](Assets/Lab2-05-Wazuh_Dashboard_Alert_92910_OneDrive_Explorer.png)
  - ![Windows FIM test file alert confirmation](Assets/Lab2-06-Windows_FIM_TestFile_C_WazuhTest_Lab2_TestFile_txt.png)

### 4. Create Custom Wazuh Rules
- Created custom XML rules:

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

- Verified rules with `wazuh-logtest`.  
- Screenshot: ![wazuh-logtest confirming rule 100101 fires correctly](Assets/Lab2-11-Wazuh_logtest_100101.png)

### 5. Verify Custom Alerts in Wazuh Dashboard
- Confirmed custom alerts appear in the Dashboard:
  - Discover view for rule 100101: ![Dashboard Discover view for custom rule 100101](Assets/Lab2-08-Discover_rule_100101.png)
  - Rule definition in Management → Rules: ![Custom rule 100101 definition in Wazuh Management → Rules](Assets/Lab2-09-Rule_definition_100101.png)

### 6. Verify Alerts in Ubuntu Terminal
- Used `tail` and `grep` to confirm custom alerts are logged in `alerts.json`.
- Screenshot: ![Terminal view showing alert for 100101 in alerts.json](Assets/Lab2-10-Alerts_terminal_100101.png)

## Summary
- Custom rules `100100` and `100101` were successfully created and tested.
- Alerts were generated and verified in both Linux and Windows environments.
- Dashboard visualizations confirmed proper integration of custom rules.
- All objectives for Lab 2 have been completed and documented.
