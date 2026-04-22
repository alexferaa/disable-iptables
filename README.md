# UFW Firewall Setup on Ubuntu 22.04

A step-by-step guide to transitioning from `iptables` to UFW (Uncomplicated Firewall) on Ubuntu 22.04.

---

## Table of Contents

1. [Disable iptables](#1-disable-iptables-and-related-services)
2. [Install UFW](#2-install-ufw)
3. [Set Default Policies](#3-set-default-policies)
4. [Allow Essential Services](#4-allow-essential-services)
5. [Enable UFW](#5-enable-ufw)
6. [Check Status](#6-check-status)
7. [Notes & Tips](#notes--tips)

---

## 1. Disable iptables (and related services)

Ubuntu 22.04 uses an `nftables` backend, but `iptables` rules may still be active. Flush and stop them first:

```bash
sudo iptables -F
sudo iptables -X
sudo iptables -t nat -F
sudo iptables -t nat -X
```

If you have persistent rules, stop and disable the service:

```bash
sudo systemctl stop netfilter-persistent
sudo systemctl disable netfilter-persistent
```

---

## 2. Install UFW

```bash
sudo apt update
sudo apt install ufw -y
```

---

## 3. Set Default Policies

Configure default policies **before** enabling UFW. The recommended baseline:

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

---

## 4. Allow Essential Services

> ⚠️ **Do this before enabling UFW** — otherwise you may lock yourself out.

Allow SSH on the default port:

```bash
sudo ufw allow ssh
```

If SSH runs on a custom port:

```bash
sudo ufw allow <port>/tcp
```

---

## 5. Enable UFW

```bash
sudo ufw enable
```

---

## 6. Check Status

```bash
sudo ufw status verbose
```

---

## Notes & Tips

- **UFW is a frontend** — it manages `iptables`/`nftables` rules under the hood; it does not remove `iptables` entirely.
- **Docker / Kubernetes** — these tools may still manipulate `iptables` rules independently of UFW.
- **Reset UFW** at any time with:

  ```bash
  sudo ufw reset
  ```
