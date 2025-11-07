\# Environment Setup

\## Overview

This project uses a virtualized lab environment to simulate a SOC setup with Wazuh SIEM and Windows endpoints.



\## Components

\- \*\*Wazuh SIEM\*\*: Deployed on Amazon Linux 2 VM (VirtualBox).

&nbsp; - Version: Wazuh 4.x

&nbsp; - Access: Web dashboard at https://<wazuh-ip>

\- \*\*Endpoint\*\*: Windows 10 Pro VM (VirtualBox).

&nbsp; - Configured with Wazuh agent for log collection.

\- \*\*Host\*\*: Windows 11, running VirtualBox 7.x.

\- \*\*Networking\*\*: Bridged adapter for VM communication.



\## Setup Steps

1\. Installed VirtualBox on Windows 11 host.

2\. Deployed Amazon Linux 2 VM, installed Wazuh all-in-one (manager, indexer, dashboard).

3\. Configured Windows 10 VM with Wazuh agent, connected to Wazuh server.

4\. Verified connectivity: Agents report to dashboard, logs visible.



\## Notes

\- Ensure VMs have internet access for package downloads.

\- Wazuh dashboard uses default credentials (change for production).

\- Back up VMs before simulations to avoid corruption.

