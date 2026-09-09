# Linux Networking Lab

This lab demonstrates basic Linux networking, including IP addressing, routing, DNS resolution, connectivity testing, listening ports, network statistics, HTTP testing, and network path troubleshooting.

---

## 1. Check IP Address

### Command

```bash
ip addr
```

### Purpose

Displays network interfaces and their assigned IP addresses.
### Lab Result
```bash
Interface: eth0
IPv4: 172.19.56.189/20
State: UP
```
## 2. Check Routing Table
### Command

```bash
ip route
```
### Purpose

Displays how Linux routes network traffic.

### Lab Result
```bash
default via 172.19.48.1 dev eth0
172.19.48.0/20 dev eth0
```
### Key Concept

172.19.48.1 is the default gateway used for traffic outside the local network.

## 3. DNS Resolution
### Command
```bash
nslookup google.com
```
### Purpose

Queries a DNS server to resolve a domain name into IP addresses.

### Lab Result
```bash
DNS Server: 10.255.255.254
google.com → IPv4 and IPv6 addresses
```
### Key Concept
Domain Name
     ↓
DNS
     ↓
IP Address
## 4. Test Internet Connectivity
### Command
```bash
ping -c 4 8.8.8.8
```
### Purpose

Tests network connectivity, latency, and packet loss.

### Lab Result
4 packets transmitted
4 packets received
0% packet loss

## 5. Test Domain Connectivity
### Command
```bash
ping -c 4 google.com
```
### Purpose

Tests both DNS resolution and network connectivity.

### Lab Result
4 packets transmitted
4 packets received
0% packet loss
## 6. Check Listening Ports
### Command
```bash
sudo ss -tulnp
```
### Purpose

Displays listening network sockets and the services using them.

### Important Ports
- 22  → SSH
- 80  → HTTP / Nginx
## 7. Check Network Interface Statistics
### Command
```bash
ip -s link show eth0
```
### Purpose

Displays network traffic statistics including received and transmitted packets, errors, and dropped packets.

### Lab Result
RX packets: 4988
RX errors: 0
RX dropped: 0

TX packets: 3144
TX errors: 0
TX dropped: 0
## 8. Test HTTP/HTTPS Connectivity
### Command
```bash
curl -I https://google.com
```
### Purpose

Tests HTTP/HTTPS connectivity and displays response headers.

### Lab Result
HTTP/2 301
location: https://www.google.com/
### Key Concept

The server successfully responded with an HTTP redirect.

## 9. Check DNS Configuration
### Command
```bash
cat /etc/resolv.conf
```
### Purpose

Displays the DNS server configured for the Linux system.

## Lab Result
nameserver 10.255.255.254
## 10. System Hostname Resolution
### Command
```bash
getent hosts google.com
```
### Purpose

Uses the Linux system name-resolution mechanism to resolve a hostname.

## 11. Test DNS Server Connectivity
### Command
```bash
ping -c 4 10.255.255.254
```
### Lab Result
4 packets transmitted
4 packets received
0% packet loss

The DNS server is reachable.

## 12. Test DNS Port
### Command
```bash
nc -zv 10.255.255.254 53
```
### Purpose

Tests whether TCP port 53 on the DNS server is reachable.

### Lab Result
Connection to 10.255.255.254 53 port [tcp/domain] succeeded!
### 13. Check Exact Route to a Destination
### Command
```bash
ip route get 8.8.8.8
```
### Purpose

Shows the exact route Linux will use to reach a specific destination.

### Lab Result
- 8.8.8.8 via 172.19.48.1 dev eth0 src 172.19.56.189
### Key Information
Destination → 8.8.8.8
Gateway     → 172.19.48.1
Interface   → eth0
Source IP   → 172.19.56.189
## 14. Trace Network Path
### Command

```bash
traceroute -m 5 8.8.8.8
```
### Purpose

Shows the network hops between the local system and the destination.

### Example Result
1.  172.19.48.1
2.  192.168.18.1
3.  '* * *'
4.  183.82.174.124
5.  14.141.149.225
## Key Concept

A * * * does not always indicate a network failure. A router may simply not respond to traceroute probes.

### Networking Troubleshooting Flow

When a website or network service is not working, troubleshoot step by step:
```bash
IP Address
    ↓
Routing
    ↓
DNS
    ↓
Connectivity
    ↓
Ports
    ↓
Application / HTTP
```
## Command Summary
| Command | Purpose |
|:------:|:------------:|
| ```ip addr```	| Check IP addresses
| ```ip route``` |	Check routing table
| ```nslookup``` |	Test DNS resolution
| ```ping```|	Test connectivity
| ```ss -tulnp```	| Check listening ports
| ```ip -s link```	| Check network statistics
| ```curl -I```	 | Test HTTP/HTTPS
| ```cat /etc/resolv.conf```	| Check DNS configuration
| ```getent hosts```	 | Test system hostname resolution
| ```nc -zv``` |	Test a specific port
| ```ip route get``` |	Check exact route
| ```traceroute```	| Trace network path
### Lab Result

Successfully inspected the Linux network interface, identified the IP address and default gateway, tested DNS resolution, verified Internet connectivity, inspected listening ports, checked network statistics, tested HTTPS connectivity, verified DNS configuration, tested DNS server port 53, inspected the exact route to a destination, and traced the network path.
### Skills Demonstrated

Linux Networking | IP Addressing | Routing | DNS | Network Connectivity | Port Troubleshooting | Network Statistics | HTTP/HTTPS Testing | Network Path Analysis | Troubleshooting
