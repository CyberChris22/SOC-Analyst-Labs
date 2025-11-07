# Lab 4: Malware Simulation and Endpoint Detection

## Objective
Simulate realistic malware data manipulation and detect it using **Wazuh FIM in real-time**, with **MITRE ATT&CK** and **compliance mapping**.

## Malware Simulation
- Created `C:\Temp\proof.txt`
- Modified file content → triggered integrity checksum change
- Mimics **T1565.001 – Stored Data Manipulation (Impact)**

## Detection
- **Rule 554:** File added (baseline)
- **Rule 550:** Realtime modification (`mode: realtime`)
- **MITRE:** T1565.001 – Stored Data Manipulation
- **Compliance:** PCI DSS 11.5, GDPR II_5.1.f, NIST SI.7, HIPAA 164.312.c.1/2

## Key Difference from Lab 2

| Lab 2                  | Lab 4                        |
|------------------------|------------------------------|
| File add/delete         | File modification            |
| Scheduled FIM           | Realtime FIM                 |
| No MITRE/Compliance     | Full mapping                 |

## Proof
- [Agent Active](./assets/lab4_agent_active.png)
- [FIM 554 – File Added](./assets/lab4_fim_554_file_added.png)
- [FIM 550 – Realtime Modified (MITRE/Compliance)](./assets/lab4_fim_550_realtime_modified.png)
- [FIM 550 – JSON Proof (mode: realtime, checksums)](./assets/lab4_fim_550_json_proof.png)

## Status
Lab 4 complete with **4 screenshots** demonstrating successful real-time detection and compliance validation.




