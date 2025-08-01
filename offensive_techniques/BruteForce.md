# FTP Brute Force Attack using Hydra

## Overview

This document explains how we performed a brute-force attack on an FTP service running on a Windows 10 virtual machine using Kali Linux and the `hydra` tool. We used **custom username and password wordlists** created for this purpose.

---

## Lab Setup

- **Attacker VM**: Kali Linux  
- **Target VM**: Windows 10 with FTP service running (IIS)  
- **Network**: Internal VirtualBox network (`intnet`), IPs:
  - Kali: `192.168.20.11`
  - Windows: `192.168.20.10`
- **FTP Service**: Configured with a known test account:
  - Username: `ftp`
  - Password: `admin`

---

## Tools Used

- `hydra` — a fast and flexible login cracker
- **Custom Wordlists**:
  - `usernames.txt`: list of possible usernames (on Kali Desktop)
  - `password.txt`: list of passwords (on Kali Desktop)

---

## Attack Execution

Hydra was used with the custom wordlists as follows:

```bash
hydra -L ~/Desktop/usernames.txt \
      -P ~/Desktop/passwords.txt \
      ftp://192.168.20.10
