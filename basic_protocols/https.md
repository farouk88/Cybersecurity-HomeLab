# HTTPS Exploration

## Overview

This document describes the observations and understanding gained from analyzing HTTPS traffic between a client (Kali VM) and a web server (e.g., google.com) using Wireshark and `curl`.

---

## Step-by-Step Traffic Flow

### 1. DNS Resolution
- The client first sends DNS queries to resolve the domain name (e.g., `google.com`) to IP addresses.
- Queries for both IPv4 (`A` record) and IPv6 (`AAAA` record) addresses are made.
- DNS server responds with the corresponding IP addresses.

### 2. TCP Handshake
- A three-way handshake occurs between the client and server to establish a reliable TCP connection:
  - **SYN:** Client initiates connection.
  - **SYN-ACK:** Server acknowledges and agrees.
  - **ACK:** Client acknowledges the server's response.

### 3. TLS Handshake (TLS 1.3 observed)
- **Client Hello:** Client proposes TLS version and cipher suites.
- **Server Hello:** Server selects TLS version and cipher suite, sends its certificate.
- **Key Exchange & Cipher Spec:** Both parties agree on encryption keys.
- **Change Cipher Spec:** Both switch to encrypted communication.
- **Finished:** Secure encrypted channel is established.

### 4. Encrypted Application Data
- Following the handshake, HTTP requests and responses are transmitted encrypted.
- Wireshark shows these as `Application Data` packets without readable content.

---

## Key Observations

- Both IPv4 and IPv6 addresses are requested during DNS resolution.
- TLS handshake occurs after TCP connection establishment.
- HTTPS traffic is encrypted, making payloads unreadable in packet captures.

---

## Tools Used

- `curl` to generate HTTPS requests.
- Wireshark to capture and analyze network packets.

---