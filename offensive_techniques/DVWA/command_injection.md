# Command Injection Attack

## Description
Injected shell commands via vulnerable input fields to execute arbitrary commands on the server.

## Example Payload
```

127.0.0.1; cat /etc/passwd

```

## Outcome
- Retrieved contents of `/etc/passwd`, exposing system user information.
- Captured the command injection in Wireshark due to unencrypted HTTP traffic.
- Obtained root-level passwords from the retrieved file.
```

---
