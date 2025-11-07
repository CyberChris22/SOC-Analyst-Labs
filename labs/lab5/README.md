# Lab 5: Basic Threat Hunting with Queries

## Overview

Lab 5 demonstrates basic threat hunting techniques using Sysmon and Wazuh (or local Windows event logs) to track suspicious activity on a Windows host. The goal is to learn how to identify potentially malicious changes to user accounts, admin groups, logon events, and DNS/network activity through targeted queries. This lab uses Sysmon for detailed system monitoring and shows how queries can detect and correlate events for threat hunting, even when Wazuh alerts may not yet trigger.

## Objectives

- Understand how to use Sysmon to monitor system events
- Run queries to detect suspicious user account and group changes
- Correlate events to investigate potential threats
- Capture and document evidence for threat hunting exercises

## Environment Setup

### 1. Sysmon Installation

```powershell
.\Sysmon64.exe -accepteula -i sysmonconfig.xml
```

- Sysmon logs process creation, file creation, registry changes, network connections, and more based on the configuration file.

- Verify installation and view the schema:

```powershell
.\Sysmon64.exe -s
```

### 2. PowerShell Event Queries

**List user account creation events**

```powershell
Get-WinEvent -LogName 'Microsoft-Windows-Sysmon/Operational' | Where-Object {$_.Id -eq 60109}
```

**List admin group changes**

```powershell
Get-WinEvent -LogName 'Microsoft-Windows-Sysmon/Operational' | Where-Object {$_.Id -eq 60154}
```

**List logon events**

```powershell
Get-WinEvent -LogName 'Security' | Where-Object {$_.Id -eq 4624}
```

**List DNS timeout events**

```powershell
Get-WinEvent -LogName 'Microsoft-Windows-DNS-Client/Operational' | Where-Object {$_.Id -eq 61109}
```

## Event Analysis & Screenshots

### 1. User Account Creation

- lab5-01_UserAccountCreated_60109.png
- lab5-01_UserAccountCreated_60109_DESKTOP-MHRV979.png

### 2. Admin Group & User Account Changes

- lab5-02_AdminGroupChanged_60154.png
- lab5-02_UserAccountChanged_60110_DESKTOP-MHRV979.png
- lab5-03_AdminsGroupChanged_60154_DESKTOP-MHRV979.png
- lab5-03_UserAccountChanged_60110.png

### 3. Event Correlation

- lab5-04_Correlation_Timeline_AccountCreationToAdmin_DESKTOP-MHRV979.png
  *(Shows timeline correlation from account creation to admin group assignment.)*

### 4. DNS / Network Events

- lab5-09_DNS_Timeout_61109_DESKTOP-MHRV979.png

### 5. Logon Events

- lab5-10_LogonEvents_4624_DESKTOP-MHRV979.png

## Lab Notes

- Queries were executed locally using PowerShell against Sysmon and Windows Security logs.
- Wazuh agent integration may not have returned alerts during this lab, but all events were successfully captured locally.
- The lab demonstrates correlating events to understand potential threat activity (e.g., tracking account creation to privilege escalation).

## Key Takeaways

- Sysmon provides granular visibility into system activity, enabling threat hunting even before centralized alerting is operational.
- Targeted queries allow analysts to identify suspicious changes such as:
  - Creation of new user accounts
  - Addition of accounts to admin groups
  - Unusual logon events
  - Network/DNS anomalies
- Correlating these events helps visualize potential attack paths.

## References

- [Sysmon Documentation](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
- [Wazuh Documentation](https://documentation.wazuh.com/current/)
