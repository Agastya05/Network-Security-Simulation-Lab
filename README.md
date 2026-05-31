# Network-Security-Simulation-Lab
Built a virtual lab using Kali Linux, Ubuntu Server, &amp; Windows 11 to simulate enterprise attack-defense scenarios. • Configured virtual network &amp; practiced security monitoring, system administration, &amp; incidence response workflows.

# Cybersecurity Operations Cyber Range & Home Lab

**Author:** Agastya Purohit
**Objective:** To architect an isolated virtual network environment for simulating adversary techniques and developing defensive incident response (DFIR) monitoring capabilities.

## 🛠️ Architecture & Technologies Used
* **Hypervisor:** VMware Workstation Pro (Type-2)
* **Virtual Networking:** Custom Host-Only Virtual Switch (VMnet2) to prevent external network leakage.
* **Attacker Profile:** Kali Linux (Debian)
* **Target Profiles:** Windows 11 Pro (Endpoint), Ubuntu Server (Headless Log Forwarder)
* **Core Tools:** Nmap, SSH, Linux command-line utilities, Windows Defender Firewall, Netplan (YAML).

## 🖧 Network Topology & Static Routing
Configured a private subnet (`10.0.0.0/24`) lacking a default gateway to ensure complete isolation from the host and internet. Assigned static IPv4 addresses to all virtual infrastructure.

| Virtual Machine | Operating System | IP Address | Role |
| :--- | :--- | :--- | :--- |
| **Kali Attacker** | Kali Linux | `10.0.0.20` | Offensive operations & network scanning |
| **Windows Endpoint** | Windows 11 Pro | `10.0.0.10` | Standard user endpoint simulation |
| **Ubuntu Server** | Ubuntu Server | `10.0.0.5` | Headless infrastructure & log aggregation |

## 🚀 Execution & Methodologies

### 1. Network Reconnaissance 
Conducted active discovery on the `10.0.0.0/24` subnet using **Nmap** (Ping Sweep). Identified live hosts while navigating Windows Defender Firewall configurations that initially dropped ICMP echo requests. 
* *Modified inbound ICMPv4 rules in `wf.msc` to allow controlled host discovery.*

[**Insert Image: Nmap_Scan_Results.png**]
*(Caption: Nmap identifying the Ubuntu server and Windows endpoint from the Kali attacker machine).*

### 2. Adversary Simulation (Brute Force)
Simulated a credential stuffing/brute force attack over the SSH protocol targeting the Ubuntu Server (`10.0.0.5`) from the Kali machine to generate actionable security events.

### 3. Log Analysis & Defensive Monitoring
Monitored the Linux authentication logs (`/var/log/auth.log`) in real-time using the `tail -f` utility. 
* Successfully identified the exact Indicators of Compromise (IoCs), including the attacker's IP address (`10.0.0.20`), the targeted service (`sshd`), and the failed authentication timestamps.

[**Insert Image: Auth_Log_Analysis.png**]
*(Caption: Real-time log capture showing failed SSH login attempts from the Kali IP).*

## 💡 Key Learnings
* **Virtualization Engineering:** Mastered thin provisioning, VM snapshots, and isolated virtual network switching.
* **Linux Administration:** Navigated headless servers, managed package repositories, and configured static routing using YAML and Netplan.
* **Security Operations:** Gained practical experience in correlating offensive network actions with their exact footprint in system logs.
