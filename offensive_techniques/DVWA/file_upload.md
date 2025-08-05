# File Upload Attack

## Description
Uploaded a malicious PHP reverse shell script through the vulnerable file upload feature.

## Steps
- Uploaded PHP shell file.
- Listened on Kali machine on port 4444 for incoming shell connection.
- Upon connection, gained remote shell access to the Debian machine.

## Privilege Escalation
- Used credentials obtained from command injection to escalate privileges to root.

## Outcome
- Full control over the target system.
````

---
