# 📡 Nagios Core Monitoring Setup

## About This Project
Built as part of my IT Security homelab to gain 
hands-on experience in infrastructure monitoring...

README
A homelab project documenting the end-to-end setup of Nagios Core infrastructure monitoring with a remote Linux client monitored via NRPE.

---

## 📋 Project Overview

| Item | Details |
|------|---------|
| **Tool** | Nagios Core 4.4.6 |
| **OS** | Ubuntu 22.04 LTS |
| **Hypervisor** | VirtualBox |
| **Network** | NAT + Host-Only Adapter |
| **Web Server** | Apache2 |
| **Monitoring Agent** | NRPE (Nagios Remote Plugin Executor) |

---

## 🖥️ Environment

```
Host Machine (Windows)
│
├── VM 1 — Nagios Server
│     IP : 192.168.56.x
│     OS : Ubuntu 22.04
│     Role: Nagios4 + Apache2
│
└── VM 2 — Client Server
      IP : 192.168.56.x
      OS : Ubuntu 22.04
      Role: NRPE + Nagios Plugins
```
---

## 🚀 Setup Phases - Network Setup

1. VirtualBox Network Configuration - Assign IP to Host-Only Interface
2. SSH Access -Install and configure SSH on client VM for remote management.
---

### Nagios4 Installation (Server)
1. Perform apt installation
2. Create admin credentials
3. Enable Apache modules
---

###  Nagios Configuration Files
1. Key files configured:
    ++ Main configuration 
    ++ CGI & web UI settings 
    ++ Plugin path ($USER1$) 
    ++ Check commands 
    ++ Admin contacts 
    ++ Monitoring schedules 
    ++ Host & service templates 
    ++ Localhost definitions 

2. Verify configuration
---

### NRPE Setup (Client VM)
1. Install NRPE on client
2. Configure nrpe.cfg
3. Allow NRPE port and start service
---

### Add Client Host to Nagios
1. Create clientservervm2.cfg
2. Restart Nagios

---

## 🔧 Troubleshooting Log

Key issues encountered and resolved during this project:

| # | Error | Root Cause | Fix |
|---|-------|-----------|-----|
| 1 | SSH: No route to host | Both VMs on NAT only | Added Host-Only adapter (Adapter 2) |
| 2 | SSH: Permission denied | Forgotten client OS password | Reset via recovery mode |
| 3 | 404 on /nagios4 | Nginx & Apache conflict | Disabled Nginx |
| 4 | Could not open password file | Wrong htpasswd path in Apache config | Updated AuthUserFile path in nagios.conf |
| 5 | nagios.cfg missing | Conflict between apt & source install | Created config file manually |
| 6 | EOF saved in config files | Heredoc command saved as line 1 | Removed with `sed -i '1d'` |
| 7 | Object config files missing | Incomplete apt install | Created all object files manually |
| 8 | Duplicate check-host-alive | Defined in both localhost.cfg & commands.cfg | Removed duplicate from localhost.cfg |
| 9 | check_nrpe not defined | Missing command definition | Added to commands.cfg |
| 10 | /var/cache/nagios4 permission error | Wrong directory ownership | Fixed with `chown nagios:nagios` |

---

## ✅ Result

- Both hosts (**localhost** and **clientserver**) showing status **UP**
- PING OK on both hosts — Packet loss = 0%
- Services monitored: PING, CPU Load, Disk Usage, Current Users
- Web UI accessible with basic authentication (nagiosadmin)
- Nagios config verified with **0 warnings, 0 errors**

---

## 📚 Full Documentation

> 📝 [View full step-by-step documentation on Notion](#) ← [https://energetic-domain-a7c.notion.site/Nagios-Monitoring-Setup-367ec53dc78880b187bcca5af04319b7]

---

## 🛠️ Skills Demonstrated

- Linux system administration
- VirtualBox network configuration
- Apache2 web server configuration
- Nagios Core installation and configuration
- NRPE remote monitoring setup
- Firewall management (UFW)
- Configuration file debugging and troubleshooting
- SSH remote access

---

## 📁 Repository Structure

```
nagios-monitoring/
├── README.md
├── configs/
│   ├── nagios.cfg
│   ├── cgi.cfg
│   ├── commands.cfg
│   ├── contacts.cfg
│   ├── timeperiods.cfg
│   ├── templates.cfg
│   ├── localhost.cfg
│   └── clientserver.cfg


*Part of my IT Security homelab portfolio. See more at [blooming2023.github.io/IT-Security-Portfolio](https://blooming2023.github.io/IT-Security-Portfolio)*
