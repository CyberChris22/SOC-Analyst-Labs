\# Lab 3: Simulating and Detecting Brute-Force Attacks on Linux



\## Objective

Simulate and detect brute-force authentication attacks on a Linux system using Wazuh. Validate log ingestion, rule triggering, and alert visualization in the Wazuh Dashboard.



\## Lab Steps and Documentation



\### 1. Verify SSH Service

\- Confirmed that the SSH service is installed, enabled, and running on the Ubuntu VM.

\- SSH service status was checked to ensure it could accept authentication attempts.

\- Screenshot:

&nbsp; - Lab3-01\_Ubuntu SSH Service Running



\### 2. Generate Failed SSH Login Attempts

\- Multiple failed SSH login attempts were generated using an invalid username.

\- These attempts were designed to simulate a brute-force authentication attack.

\- Failed login events were written to /var/log/auth.log.

\- Screenshots:

&nbsp; - Lab3-02\_Ubuntu auth.log failed SSH logins

&nbsp; - Lab3-02\_Ubuntu auth.log failed SSH logins

&nbsp; - Lab3-02\_Ubuntu auth.log failed SSH logins



\### 3. Verify Log Ingestion and Rule Triggering

\- Wazuh successfully ingested SSH authentication logs from the Ubuntu system.

\- Failed login attempts were decoded correctly by the SSH decoder.

\- Wazuh triggered the built-in rule for invalid SSH login attempts:

&nbsp; - Rule ID: 5710

&nbsp; - Description: sshd: Attempt to login using a non-existent user

\- MITRE ATT\&CK techniques detected:

&nbsp; - T1110.001 – Password Guessing

&nbsp; - T1021.004 – SSH



\### 4. Verify Alerts in Wazuh Dashboard

\- Confirmed that SSH failed login alerts appeared in the Wazuh Dashboard.

\- Alerts displayed source IP address, username, rule ID, severity level, and MITRE mappings.

\- Screenshot:

&nbsp; - Lab3-05\_Wazuh Dashboard SSH Failed Login Alert



\## Summary

\- SSH service was verified as running on the Ubuntu VM.

\- Failed SSH login attempts successfully simulated a brute-force attack.

\- Authentication failures were logged in auth.log and ingested by Wazuh.

\- Wazuh rules triggered correctly and generated alerts.

\- Alerts were verified in the Wazuh Dashboard.

\- All Lab 3 objectives were fully met and documented.



\## Skills Demonstrated

\- Linux SSH authentication monitoring

\- Brute-force attack simulation

\- Wazuh log ingestion and decoding

\- Rule triggering and alert validation

\- MITRE ATT\&CK technique mapping



