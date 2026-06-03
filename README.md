# 🖥️ Born2beRoot

A 42 project setting up a secure Linux server from scratch inside a Virtual Machine.

---

## Introduction

Born2beRoot is a system administration project.  
The goal is to configure a **Debian** virtual machine following strict security rules, with no graphical interface — everything is done through the command line.

> **The signature of this project is the VM itself** — the virtual machine file is what gets evaluated, not source code.

### Key Concepts

- **Debian** — Linux distribution used for the server
- **LVM** — Logical Volume Manager for disk partitioning
- **UFW** — Uncomplicated Firewall to control network access
- **SSH** — Secure Shell for remote access on port 4242
- **User & group management** — creating users, assigning groups and permissions
- **Password policy** — enforcing strong password rules via PAM
- **Sudo configuration** — restricting and logging sudo usage
- **Cron** — scheduling the `monitoring.sh` script every 10 minutes
- **monitoring.sh** — a bash script that displays system information

---

## Configuration

### Partitioning

The disk is partitioned using **LVM** with encrypted partitions as required by the subject.

### Services

| Service | Status | Description |
|---|---|---|
| `SSH` | Active | Listening on port **4242** only |
| `UFW` | Active | Only port 4242 open |
| `sudo` | Configured | Restricted usage with logging |

### Password Policy

- Minimum **10 characters**
- Must contain **uppercase**, **lowercase**, and **numbers**
- Cannot contain more than **3 consecutive identical characters**
- Expires every **30 days**
- Minimum **2 days** before a password can be changed
- Warning **7 days** before expiration

### Sudo Rules

- Authentication limited to **3 attempts**
- Custom error message on wrong password
- All sudo inputs/outputs logged in `/var/log/sudo/`
- TTY mode enabled
- Restricted paths for sudo usage

---

## monitoring.sh

A bash script that runs every **10 minutes** via cron and broadcasts system information to all terminals :

```
# Architecture and kernel version
# Number of physical and virtual CPUs
# RAM usage
# Disk usage
# CPU load
# Last reboot date
# LVM status
# Active connections
# Number of logged-in users
# Network info (IP and MAC address)
# Number of sudo commands executed
```

---

## Author

Made by [Arthur-PRZ](https://github.com/Arthur-PRZ)
