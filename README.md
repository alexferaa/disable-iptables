# 🔐 Firewall Setup Guide (Ubuntu 22.04)

![Ubuntu](https://img.shields.io/badge/OS-Ubuntu%2022.04-E95420?logo=ubuntu)
![Firewall](https://img.shields.io/badge/Firewall-UFW-blue)
![Status](https://img.shields.io/badge/Status-Working-brightgreen)

A simple guide to disable `iptables`, enable `ufw`, and allow HTTP (port 80) and HTTPS (port 443). Includes troubleshooting steps for connectivity issues.

---

## 📚 Table of Contents

- [1. Disable iptables](#1-disable-iptables)
- [2. Install UFW](#2-install-ufw)
- [3. Configure Default Policies](#3-configure-default-policies)
- [4. Allow Required Ports](#4-allow-required-ports)
- [5. Enable UFW](#5-enable-ufw)
- [6. No Reboot Required](#6-no-reboot-required)
- [7. Troubleshooting](#7-troubleshooting)
- [8. Python Port Check Script](#8-python-port-check-script)
- [Summary](#summary)

---

## 1. Disable iptables

Flush all existing rules:

```bash id="5l3b6r"
sudo iptables -F
sudo iptables -X
sudo iptables -t nat -F
sudo iptables -t nat -X
