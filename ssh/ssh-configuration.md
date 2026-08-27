# SSH Administration

This lab demonstrates OpenSSH server management, SSH service control, port verification, and Ed25519 key-based authentication on Ubuntu 24.04 LTS using WSL2.

## Environment

- OS: Ubuntu 24.04 LTS
- Platform: WSL2
- SSH Server: OpenSSH
- SSH Port: 22
- Authentication: Ed25519 SSH Key

---

## 1. Check SSH Version

```bash
ssh -V
```

This verifies that the OpenSSH client is installed.

---

## 2. Install OpenSSH Server

```bash
sudo apt update
sudo apt install openssh-server
```

Verify the SSH service:

```bash
sudo systemctl status ssh
```

---

## 3. Start and Stop SSH Service

Start SSH:

```bash
sudo systemctl start ssh
```

Stop SSH:

```bash
sudo systemctl stop ssh
```

Restart SSH:

```bash
sudo systemctl restart ssh
```

Check status:

```bash
sudo systemctl status ssh
```

---

## 4. Verify SSH Port

Check whether SSH is listening on port 22:

```bash
sudo ss -tlnp | grep :22
```

Expected:

```text
0.0.0.0:22
[::]:22
```

This confirms that the SSH server is listening on TCP port 22.

---

## 5. SSH Service Logs

View recent SSH logs:

```bash
sudo journalctl -u ssh --no-pager -n 20
```

View logs since boot:

```bash
sudo journalctl -u ssh -b --no-pager
```

These logs help troubleshoot SSH service start, stop, and connection-related events.

---

## 6. Generate Ed25519 SSH Key

Generate an SSH key pair:

```bash
ssh-keygen -t ed25519
```

The key pair contains:

```text
Private Key → ~/.ssh/id_ed25519
Public Key  → ~/.ssh/id_ed25519.pub
```

### Important

The private key must never be shared.

---

## 7. Configure authorized_keys

Create the SSH directory for the `devopsks` user:

```bash
sudo mkdir -p /home/devopsks/.ssh
```

Copy the public key:

```bash
sudo cp ~/.ssh/id_ed25519.pub /home/devopsks/.ssh/authorized_keys
```

Set ownership:

```bash
sudo chown -R devopsks:devopsks /home/devopsks/.ssh
```

Set secure permissions:

```bash
sudo chmod 700 /home/devopsks/.ssh
sudo chmod 600 /home/devopsks/.ssh/authorized_keys
```

---

## 8. Test SSH Key Authentication

Connect as the `devopsks` user:

```bash
ssh -i ~/.ssh/id_ed25519 -o IdentitiesOnly=yes devopsks@localhost
```

After successful authentication:

```bash
whoami
```

Expected:

```text
devopsks
```

This confirms that SSH key-based authentication is working.

---

## 9. SSH Authentication Flow

```text
Client
  |
  | Private Key
  v
SSH Server :22
  |
  | checks Public Key
  v
/home/devopsks/.ssh/authorized_keys
  |
  v
Authentication Successful
  |
  v
devopsks Shell
```

---

## Key Concepts

| Concept | Meaning |
|---|---|
| SSH | Secure remote administration protocol |
| sshd | OpenSSH server process |
| Port 22 | Default SSH port |
| Private Key | Secret key stored on client |
| Public Key | Key placed on server |
| authorized_keys | Stores allowed public keys |
| Ed25519 | Modern SSH public-key algorithm |
| systemctl | Manages system services |
| journalctl | Reads systemd service logs |

---

## Security Notes

- Never share the private SSH key.
- Protect `.ssh` with `700` permissions.
- Protect `authorized_keys` with `600` permissions.
- Use SSH key authentication instead of passwords where possible.
- Verify SSH firewall rules before disabling password access.

---

## Lab Result

Successfully installed and managed OpenSSH, verified SSH port 22, generated an Ed25519 key pair, configured `authorized_keys`, and successfully tested passwordless SSH key-based authentication for the `devopsks` user.
