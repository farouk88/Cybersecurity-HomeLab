**File: `enumeration/nmap/README.md`**

```markdown
# Nmap

Nmap is used for network discovery and service enumeration.  

## Files

- `commands.txt` : contains the Nmap commands executed  
- `1.txt`, `2.txt`, ... : outputs of the commands

## Common Flags

- `-p` : specific port or port range  
- `-p-` : all ports  
- `-F` : top 100 ports  
- `-oN` : output file  
- `-sC` : run default scripts (e.g., detect service info)  
- `-sV` : version detection (e.g., Apache 2.4.62, ProFTPD)  
- `-sS` : SYN scan (stealthy, default for root)  
- `-sT` : TCP connect scan (less stealthy)  
- `-sU` : UDP scan  
- `-O` : OS detection  
- `-A` : aggressive mode (`-sC -sV -O -traceroute`)  
- `--script=http-enumerate` : enumerate HTTP services  
- `--script=vuln` : run vulnerability scripts  
- `-traceroute` : discover network path
```

---