🏠 Home Lab: pfSense | Active Directory | Sysmon | CrowdSec
📌 Project Overview

This project simulates a small enterprise IT environment with a focus on network segmentation, identity management, and endpoint monitoring.

The lab demonstrates:

🔹 Configuring a firewall with pfSense.

🔹 Deploying Active Directory for centralized identity management.

🔹 Adding a Windows 10 workstation to the domain.

🔹 Installing Sysmon for endpoint logging.

🔹 Deploying CrowdSec for log-based intrusion detection.

The goal is to create a realistic environment for security monitoring, detection, and analysis.

🏗️ Lab Architecture
Network Topology
               +---------------------+
               |      Internet       |
               +---------------------+
                        |
                        v
               +---------------------+
               |       pfSense       |
               |  WAN: DHCP          |
               |  LAN: 192.168.1.1   |
               |  DMZ: 192.168.2.1   |
               +---------------------+
                        |
         ------------------------------------
         |                                  |
+--------------------+            +----------------------+
| Windows Server 2019|            | Windows 10 Workstation|
| Active Directory   |            | Domain-joined client |
| Domain: SOC.LAB    |            | User logins tested   |
| IP: 192.168.1.3    |            | IP: 192.168.1.2      |
+--------------------+            +----------------------+

⚙️ Deployment Steps
1️⃣ pfSense

Configured WAN as DHCP.

Assigned LAN → 192.168.1.1/24.

Configured DMZ interface → 192.168.2.1/24.

Verified access to pfSense Web UI from LAN.

2️⃣ Active Directory (Windows Server 2019)

Installed Active Directory Domain Services.

Created new domain: SOC.LAB.

Populated users & groups using BadBlood
 to simulate a realistic enterprise environment.

3️⃣ Windows 10 Workstation

Assigned static IP → 192.168.1.2.

Joined to SOC.LAB domain.

Verified logon with domain users.

4️⃣ Sysmon

Installed Sysmon on both server and workstation.

Used Olaf Hartong’s Sysmon Modular Config
.

Verified logs in Event Viewer → Applications and Services Logs → Microsoft → Windows → Sysmon/Operational.

5️⃣ CrowdSec

Installed CrowdSec agent on the Windows 10 workstation.

Installed Windows collection:

cscli collections install crowdsecurity/windows


Restarted CrowdSec service:

Restart-Service CrowdSec


Verified metrics with:

cscli metrics


Set CrowdSec to automatic startup.

🧪 Testing & Results

Failed logins from test accounts were captured in Windows Event Logs.

Sysmon provided detailed process creation & authentication logs.

CrowdSec successfully parsed Windows events and detected suspicious behavior.

Validated end-to-end visibility: Log Generation → Collection → Detection.
