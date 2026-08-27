# Nginx Web Server Administration

This lab demonstrates Nginx installation, service management, HTTP port configuration, firewall rules, port verification, and custom web page deployment.

## Environment

- OS: Ubuntu 24.04 LTS
- Platform: WSL2
- Web Server: Nginx
- Protocol: HTTP
- HTTP Port: 80
- Firewall: UFW

---

## 1. Install Nginx

Update package information:

```bash
sudo apt update
```

Install Nginx:

```bash
sudo apt install nginx
```

Verify installation:

```bash
nginx -v
```

---

## 2. Check Nginx Service

Check Nginx status:

```bash
sudo systemctl status nginx
```

Expected:

```text
Active: active (running)
```

This confirms that the Nginx web server is running.

---

## 3. Nginx Configuration Test

Test the Nginx configuration:

```bash
sudo nginx -t
```

Expected:

```text
syntax is ok
test is successful
```

---

## 4. Verify HTTP Port 80

Check whether Nginx is listening on port 80:

```bash
sudo ss -tlnp | grep :80
```

Expected:

```text
0.0.0.0:80
[::]:80
```

This confirms that Nginx is listening for HTTP traffic.

---

## 5. Test Nginx with curl

Test the local web server:

```bash
curl http://localhost
```

The HTTP response confirms that Nginx is serving web content successfully.

---

## 6. Configure UFW Firewall

Check firewall status:

```bash
sudo ufw status numbered
```

Allow SSH:

```bash
sudo ufw allow 22/tcp
```

Allow HTTP:

```bash
sudo ufw allow 80/tcp
```

Enable UFW:

```bash
sudo ufw enable
```

Verify the firewall:

```bash
sudo ufw status verbose
```

Expected rules:

```text
22/tcp   ALLOW IN   Anywhere
80/tcp   ALLOW IN   Anywhere
22/tcp   ALLOW IN   Anywhere (v6)
80/tcp   ALLOW IN   Anywhere (v6)
```

---

## 7. Custom Web Page

A custom HTML page was deployed for the Linux Server Administration lab.

Example content:

```html
<h1>Linux Server Administration</h1>
<p>Nginx is successfully serving this page.</p>
<p>Server Environment: Ubuntu 24.04 LTS + WSL2</p>
```

The page was tested through:

```text
http://localhost
```

Browser result:

```text
Linux Server Administration

Nginx is successfully serving this page.

Server Environment: Ubuntu 24.04 LTS + WSL2
```

---

## 8. Nginx Service Management

Start Nginx:

```bash
sudo systemctl start nginx
```

Stop Nginx:

```bash
sudo systemctl stop nginx
```

Restart Nginx:

```bash
sudo systemctl restart nginx
```

Check status:

```bash
sudo systemctl status nginx
```

---

## 9. Nginx Logs

View recent Nginx service logs:

```bash
sudo journalctl -u nginx --no-pager -n 20
```

Logs can be used to troubleshoot service startup and runtime problems.

---

## Architecture

```text
Browser
   |
   | HTTP :80
   v
UFW Firewall
   |
   | ALLOW 80/tcp
   v
Nginx Web Server
   |
   v
Web Root
   |
   v
HTML Page
   |
   v
HTTP Response
```

---

## Troubleshooting Commands

### Check Nginx status

```bash
sudo systemctl status nginx
```

### Test configuration

```bash
sudo nginx -t
```

### Check port 80

```bash
sudo ss -tlnp | grep :80
```

### Test HTTP response

```bash
curl http://localhost
```

### Check Nginx logs

```bash
sudo journalctl -u nginx --no-pager -n 20
```

### Check firewall

```bash
sudo ufw status numbered
```

---

## Key Concepts

| Concept | Meaning |
|---|---|
| Nginx | Web server |
| HTTP | Web communication protocol |
| Port 80 | Default HTTP port |
| systemctl | Service management |
| ss | Network socket/port verification |
| curl | Command-line HTTP client |
| UFW | Ubuntu firewall |
| journalctl | systemd log viewer |
| Web Root | Directory containing web files |

---

## Lab Result

Successfully installed and configured Nginx, verified the Nginx service, confirmed HTTP port 80, configured UFW to allow HTTP traffic, tested the server using `curl`, and deployed a custom Linux Server Administration web page.
