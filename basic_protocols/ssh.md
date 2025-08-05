# SSH Key-Based Authentication Setup and Exploration

## Setup Overview

This experiment demonstrates setting up SSH key-based authentication between a **Kali (attacker/client)** machine and a **Debian (server)** machine on a local internal network.

---

## Environment

- **Kali (client)**: `192.168.20.11`
- **Debian (SSH server)**: `192.168.20.12`

---

## Step-by-Step Instructions

### 1. Enable & Start SSH Server on Debian

On the Debian machine:

```bash
sudo systemctl enable ssh
sudo systemctl start ssh
````

This ensures the SSH server (`sshd`) is active and will start on boot.

---

### 2. Generate SSH Key Pair on Kali

On the Kali machine:

```bash
ssh-keygen -t rsa
```

This generates two files in the `~/.ssh/` directory:

* `id_rsa`: Private key (keep secret)
* `id_rsa.pub`: Public key (can be shared)

---

### 3. Copy Public Key to Debian (Server)

From Kali:

```bash
ssh-copy-id 192.168.20.12
```

You will be prompted to enter Debian's user password one last time. This command appends Kali's public key to:

```bash
~/.ssh/authorized_keys
```

on the Debian machine, allowing passwordless SSH from Kali.

---

### 4. Connect to SSH Server

Now you can connect securely without entering the password:

```bash
ssh 192.168.20.12
```

---

## Key File Inspection

On Kali:

* View private key:

  ```bash
  cat ~/.ssh/id_rsa
  ```

* View public key:

  ```bash
  cat ~/.ssh/id_rsa.pub
  ```

---

## SSH Server Configuration (Debian)

SSH server settings are located in:

```bash
/etc/ssh/sshd_config
```

Key directives include:

* `Port 22` — default SSH port
* `PermitRootLogin` — controls root login access
* `PubkeyAuthentication yes` — enables public key auth
* `AuthorizedKeysFile .ssh/authorized_keys` — file path for authorized keys

Changes require:

```bash
sudo systemctl restart ssh
```

---

## Result

After setup, Kali can connect to Debian using key-based authentication with:

```bash
ssh 192.168.20.12
```

No password is required thanks to the public key being authorized on the Debian SSH server.

---

```
