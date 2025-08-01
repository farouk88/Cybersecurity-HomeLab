# Network Basics & Service Interactions

This document summarizes the experiments and observations made while setting up and testing network communication between a Kali Linux VM and a Windows 10 VM.

## Setup

- **Internal network**: `intnet`
- **Kali IP**: `192.168.20.11`
- **Windows IP**: `192.168.20.10`

---

## 1. Connectivity Tests (ICMP Ping)

- Confirmed that both machines could reach each other using `ping`
- Observed the ICMP Echo Request and Echo Reply messages in Wireshark

---

## 2. TCP Handshake via Netcat

- Opened port **4444** on Windows using `ncat -lvp 4444`
- Connected from Kali using `nc 192.168.20.10 4444`
- Observed:
  - SYN → SYN-ACK → ACK: Standard 3-way TCP handshake
  - Exchanged text messages and verified data transmission
- Wireshark insights:
  - Saw PSH, ACK flags used for pushing text messages
  - Connection teardown involved FIN or RST packets

---

## 3. HTTP Service

- Started Python HTTP server on Windows: `python -m http.server 80`
- Accessed from Kali using `curl http://192.168.20.10`
- Observed:
  - `GET / HTTP/1.1` request
  - `HTTP/1.0 200 OK` with HTML content in response
- Wireshark:
  - Clear-text headers and body
  - Demonstrated how unencrypted HTTP reveals all content

---

## 4. FTP Service

- Set up FTP on Windows using IIS
- Created user `ftpuser` with password `ftp`
- Connected from Kali: `ftp 192.168.20.10`
- Logged in and observed the command flow:
  - USER → PASS → 230 User logged in
  - EPSV and data connection on port 17778
- Wireshark:
  - FTP credentials sent in plaintext
  - Passive mode data port negotiation visible
  - Saw attempted file transfer initiation

---

## Key Takeaways

- Basic services like FTP and HTTP are **highly insecure** over plaintext.
- Packet captures offer deep visibility into every step of the communication.
- Understanding protocol mechanics is critical for both defense and offense.
- Passive FTP requires careful port configuration to work properly in NAT or firewalled environments.

---

## Resources

- Wireshark [Display Filters Cheat Sheet](https://www.wireshark.org/docs/dfref/)
- Netcat (`nc` or `ncat`) for quick server/client TCP
- Python HTTP Server module
