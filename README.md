# Cybersecurity HomeLab

This repository documents a personal cybersecurity and networking lab built using VirtualBox VMs, designed to explore hands-on concepts in networking, traffic analysis, and security protocols.

## Goals

- Understand network protocols (TCP, IP, FTP, HTTP) at a packet level
- Analyze network traffic with Wireshark
- Simulate common client-server interactions
- Explore security implications of plaintext protocols
- Build foundational knowledge for offensive and defensive security

## Lab Setup

- **Virtual Machines**:
  - Kali Linux (Attacker/Analyst)
  - Windows 10 (Victim/Server)
- **Network**: Internal VirtualBox network (`intnet`)
- **IP Configuration**:
  - Kali: `192.168.20.11`
  - Windows: `192.168.20.10`

## Themes

- `network-basics/`: Core network services and protocols (ping, TCP, HTTP, FTP)
- `traffic-analysis/`: Packet captures and insights with Wireshark
- `protocol-analysis/`: Observations of handshakes, data exchange, and weaknesses
- *(To be added)* `offensive-techniques/`: Scanning, enumeration, and exploitation
- *(To be added)* `defensive-techniques/`: Monitoring, firewalls, detection

## Contents

- `network-basics.md` — Setup and experiments with ping, nc, ftp, http
- `captures/` — Wireshark `.pcapng` files for each task
- `screenshots/` — Wireshark screenshots, command-line outputs

## Tools Used

- [Wireshark](https://www.wireshark.org/)
- [Netcat / Ncat](https://nmap.org/ncat/)
- [Python SimpleHTTPServer](https://docs.python.org/)
- [VirtualBox](https://www.virtualbox.org/)
- Kali Linux, Windows 10

---

## 🚧 Status

This is a work in progress. More themes will be added (scanning, exploits, etc.) as the lab evolves.

---