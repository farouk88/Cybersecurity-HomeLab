# DNS Exploration and Packet Analysis

## Objective
To understand how DNS resolution works by querying both internal and external DNS services, and observing the corresponding DNS packets using network capture tools.

## Tools Used
- **dig**: Command-line tool to perform DNS lookups and query specific DNS record types.
- **nslookup**: Interactive DNS query tool.
- **Wireshark**: Network protocol analyzer to capture and analyze DNS traffic.

## Steps Performed

1. **Query Internal DNS:**
   - Used `dig` to query local DNS servers for IPv4 (`A`) and IPv6 (`AAAA`) records of domains such as `google.com`.
   - Example commands:
     ```bash
     dig A google.com
     dig AAAA google.com
     ```
   - Verified results with `nslookup`:
     ```bash
     nslookup google.com
     ```

2. **Query External DNS:**
   - Queried external DNS servers to resolve internal hostnames.
   - Example commands:
     ```bash
     nslookup google.com 8.8.8.8
     ```

3. **Capture and Analyze DNS Traffic:**
   - Captured DNS packets on network interfaces using Wireshark.
   - Observed DNS queries (Standard query) and responses (Standard query response).
   - Examined packet details such as:
     - Transaction ID
     - Query Name
     - Query Type (A or AAAA)
     - Answer IP addresses

## Observations
- DNS servers return both IPv4 and IPv6 addresses, showing dual-stack DNS support.
- DNS traffic packets can be identified and inspected easily in Wireshark.
- DNS resolution is critical for converting human-friendly domain names to IP addresses, enabling network communication.


