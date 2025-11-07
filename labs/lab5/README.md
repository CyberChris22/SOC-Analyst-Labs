\# Lab 5: Basic Threat Hunting with Queries



\## Overview

Lab 5 demonstrates basic threat hunting techniques using Sysmon and Wazuh (or local Windows event logs) to track suspicious activity on a Windows host. The goal of this lab is to learn how to identify potentially malicious changes to user accounts, admin groups, logon events, and DNS/network activity through targeted queries. This lab uses Sysmon for detailed system monitoring and shows how queries can detect and correlate events for threat hunting, even in cases where Wazuh alerts may not yet trigger.



\## Objectives

\- Understand how to use Sysmon to monitor system events.

\- Run queries to detect suspicious user account and group changes.

\- Correlate events to investigate potential threats.

\- Capture and document evidence for threat hunting exercises.



\## Environment Setup

1\. Sysmon Installation:

&nbsp;  .\\Sysmon64.exe -accepteula -i sysmonconfig.xml

&nbsp;  - Sysmon logs process creation, file creation, registry changes, network connections, and more based on the configuration file.

&nbsp;  - Verify installation and view the schema:

&nbsp;  .\\Sysmon64.exe -s



2\. PowerShell Event Queries:

&nbsp;  # List user account creation events

&nbsp;  Get-WinEvent -LogName 'Microsoft-Windows-Sysmon/Operational' | Where-Object {$\_.Id -eq 60109}



&nbsp;  # List admin group changes

&nbsp;  Get-WinEvent -LogName 'Microsoft-Windows-Sysmon/Operational' | Where-Object {$\_.Id -eq 60154}



&nbsp;  # List logon events

&nbsp;  Get-WinEvent -LogName 'Security' | Where-Object {$\_.Id -eq 4624}



&nbsp;  # List DNS timeout events

&nbsp;  Get-WinEvent -LogName 'Microsoft-Windows-DNS-Client/Operational' | Where-Object {$\_.Id -eq 61109}



\## Event Analysis \& Screenshots

Below are example events captured during the lab:



1\. User Account Creation:

&nbsp;  - lab5-01\_UserAccountCreated\_60109

&nbsp;  - lab5-01\_UserAccountCreated\_60109\_DESKTOP-MHRV979



2\. Admin Group \& User Account Changes:

&nbsp;  - lab5-02\_AdminGroupChanged\_60154

&nbsp;  - lab5-02\_UserAccountChanged\_60110\_DESKTOP-MHRV979

&nbsp;  - lab5-03\_AdminsGroupChanged\_60154\_DESKTOP-MHRV979

&nbsp;  - lab5-03\_UserAccountChanged\_60110



3\. Event Correlation:

&nbsp;  - lab5-04\_Correlation\_Timeline\_AccountCreationToAdmin\_DESKTOP-MHRV979 (Shows timeline correlation from account creation to admin group assignment)



4\. DNS / Network Events:

&nbsp;  - lab5-09\_DNS\_Timeout\_61109\_DESKTOP-MHRV979



5\. Logon Events:

&nbsp;  - lab5-10\_LogonEvents\_4624\_DESKTOP-MHRV979



\## Lab Notes

\- Queries were executed locally using PowerShell against Sysmon and Windows Security logs.

\- Wazuh agent integration may not have returned alerts during this lab, but all events were successfully captured locally.

\- The lab demonstrates the correlation of events to understand potential threat activity (e.g., tracking account creation to privilege escalation).



\## Key Takeaways

\- Sysmon provides granular visibility into system activity, enabling threat hunting even before centralized alerting is fully operational.

\- Targeted queries allow analysts to identify suspicious changes such as:

&nbsp; - Creation of new user accounts

&nbsp; - Addition of accounts to admin groups

&nbsp; - Unusual logon events

&nbsp; - Network/DNS anomalies

\- Correlation of these events helps visualize potential attack paths.



\## References

\- Sysmon Documentation: https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon

\- Wazuh Documentation: https://documentation.wazuh.com/current/



