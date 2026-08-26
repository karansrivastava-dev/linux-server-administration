# SSH Administration

A hands-on SSH administration lab covering OpenSSH installation, SSH service management, port verification, SSH connections, and key-based authentication.

## Environment

- OS: Ubuntu 24.04 LTS
- Platform: WSL2
- SSH: OpenSSH
- SSH Port: 22
- Test User: devopsks

## 1. Install OpenSSH Client

Installed the OpenSSH client for connecting to SSH servers.

### Command

```bash
sudo apt update
sudo apt install openssh-client -y
```
### Verify

```bash
ssh -V
```
## 2. Install OpenSSH Server

Installed the OpenSSH server to allow incoming SSH connections.

### Command

```bash
sudo apt install openssh-server -y
```
### Start SSH Service
```bash
sudo systemctl start ssh
```
### Check SSH Service
```bash
sudo systemctl status ssh
```
## 3. Verify SSH Port
SSH uses port 22 by default.
### Command
```bash
sudo ss -tlnp | grep :22
```
### Result

The SSH daemon was listening on port 22 for IPv4 and IPv6 connections.
## 4. Test SSH Connection

Tested a local SSH connection using:
###  Command
```bash
ssh localhost
```
Verified the logged-in user:
```bash
whoami
```
## 5. SSH Key Authentication

An Ed25519 SSH key pair was used for key-based authentication.

### Key Files
```bash
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
```
## 6. Configure Authorized Keys
Created the SSH directory for the devopsks user:
### Command
```bash
sudo mkdir -p /home/devopsks/.ssh
```
Copied the public key to authorized_keys:
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
## 7. Test Key-Based Authentication

Connected to the devopsks user using the Ed25519 private key:
### Command
```bash
ssh -i ~/.ssh/id_ed25519 -o IdentitiesOnly=yes devopsks@localhost
```
The connection successfully authenticated without asking for the user's password.

Verified the logged-in user:
```bash
whoami
```

Expected output:
```bash
devopsks
```
## Skills Demonstrated

- OpenSSH Client and Server
- SSH service management
- SSH port 22
- Local SSH connections
- Ed25519 SSH keys
- Public and private key authentication
- `authorized_keys`
- Linux file permissions
- Linux ownership
- Passwordless SSH authentication

## Key Concepts

```text
SSH Client
     |
     | Private Key
     v
SSH Server :22
     |
     | Public Key
     v
authorized_keys
     |
     v
Authentication
     |
     v
Shell Access
```
## Lab Result

Successfully configured and tested SSH key-based authentication between the local WSL environment and the devopsks user.
