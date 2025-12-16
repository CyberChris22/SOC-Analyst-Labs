\# Lab 3: Simulating and Detecting Brute-Force Attacks on Linux



\## Objective

Simulate and detect SSH brute-force authentication attacks on a Linux host using Wazuh. Validate that logs are ingested, rules trigger correctly, and alerts appear in the Wazuh Dashboard.



\## Lab Steps and Documentation



\### 1. Verify SSH Service Running

\- Confirmed the SSH service is active on Ubuntu VM.

\- \*\*Screenshot:\*\* `Lab3-01\_Ubuntu\_SSH\_Service\_Running`



\### 2. Generate Failed SSH Login Attempts

\- Performed multiple SSH login attempts using invalid usernames to simulate brute-force activity.

\- Sample log entries from `/var/log/auth.log`:

&nbsp; - Dec 15 18:23:00 UbuntuVM sshd\[1234]: Failed password for invalid user test from 127.0.0.1 port 55555 ssh2

&nbsp; - Dec 15 18:23:02 UbuntuVM sshd\[1235]: Failed password for invalid user test2 from 127.0.0.1 port 55556 ssh2

&nbsp; - Dec 15 18:23:04 UbuntuVM sshd\[1236]: Failed password for invalid user test3 from 127.0.0.1 port 55557 ssh2

\- \*\*Screenshots:\*\*

&nbsp; - `Lab3-02\_Ubuntu\_authlog\_failed\_SSH\_login\_1`

&nbsp; - `Lab3-03\_Ubuntu\_authlog\_failed\_SSH\_login\_2`

&nbsp; - `Lab3-04\_Ubuntu\_authlog\_failed\_SSH\_login\_3`



\### 3. Verify Log Ingestion in Wazuh

\- Wazuh successfully ingested the failed SSH login events from `auth.log`.

\- Alerts were decoded and rules matched automatically (rule ID `5710` for failed login attempts).



\### 4. Confirm Alerts in Wazuh Dashboard

\- Navigated to \*\*Security Events / Discover\*\* in Wazuh Dashboard.

\- Verified that all failed login attempts triggered alerts.

\- \*\*Screenshot:\*\* `Lab3-05\_Wazuh\_Dashboard\_SSH\_Failed\_Login\_Alert`



\## Outcomes

\- Linux SSH brute-force simulation completed.

\- Wazuh successfully detected all failed login attempts.

\- Alerts were verified in the dashboard, confirming proper rule configuration and log ingestion.



\## Skills Demonstrated

\- MITRE ATT\&CK T1078 (Valid Accounts) detection via SSH brute-force simulation.

\- Linux log monitoring and analysis (`auth.log`).

\- Wazuh rule triggering, alert verification, and dashboard validation.

\- End-to-end SIEM correlation for failed login events.



