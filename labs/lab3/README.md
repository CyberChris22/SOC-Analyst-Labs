# Lab 3: Simulating and Detecting Brute-Force Attacks on Linux

## Objective
Simulate and detect SSH brute-force authentication attacks on a Linux host using Wazuh. Validate log ingestion, rule triggering, and alert appearance in the Wazuh Dashboard.

## Lab Steps and Documentation

### 1. Verify SSH Service Running
- Confirmed the SSH service is active on Ubuntu VM.
- **Screenshot:** Lab3-01_Ubuntu SSH Service Running

### 2. Generate Failed SSH Login Attempts
- Performed multiple SSH login attempts using invalid usernames to simulate brute-force activity.
- Sample log entries from `/var/log/auth.log`:
Dec 15 18:23:00 UbuntuVM sshd[1234]: Failed password for invalid user test from 127.0.0.1 port 55555 ssh2  
Dec 15 18:23:02 UbuntuVM sshd[1235]: Failed password for invalid user test2 from 127.0.0.1 port 55556 ssh2  
Dec 15 18:23:04 UbuntuVM sshd[1236]: Failed password for invalid user test3 from 127.0.0.1 port 55557 ssh2  
Dec 15 18:23:06 UbuntuVM sshd[1237]: Failed password for invalid user test4 from 127.0.0.1 port 55558 ssh2  
Dec 15 18:23:08 UbuntuVM sshd[1238]: Failed password for invalid user test5 from 127.0.0.1 port 55559 ssh2  
Dec 15 18:23:10 UbuntuVM sshd[1239]: Failed password for invalid user test6 from 127.0.0.1 port 55560 ssh2  

- **Screenshots:**  
  Lab3-02_Ubuntu auth.log failed SSH logins  
  Lab3-03_Ubuntu auth.log failed SSH logins  
  Lab3-04_Ubuntu auth.log failed SSH logins

### 3. Verify Log Ingestion in Wazuh
- Wazuh successfully ingested the failed SSH login events from `auth.log`.
- Alerts were decoded and matched by **rule ID 5710** (`sshd: Attempt to login using a non-existent user`).

### 4. Confirm Alerts in Wazuh Dashboard
- Navigated to **Security Events / Discover** in Wazuh Dashboard.
- Verified all failed login attempts triggered alerts.
- **Screenshot:** Lab3-05_Wazuh Dashboard SSH Failed Login Alert

## Outcomes
- Linux SSH brute-force simulation completed.
- Wazuh detected all failed login attempts successfully.
- Dashboard confirmed proper rule configuration and alert ingestion.

## Skills Demonstrated
- MITRE ATT&CK **T1078 (Valid Accounts)** detection via SSH brute-force simulation.
- Linux log monitoring and analysis (`auth.log`).
- Wazuh rule triggering, alert verification, and dashboard validation.
- End-to-end SIEM correlation for failed login events.

