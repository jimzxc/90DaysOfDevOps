Use this as your cleaned day-14-networking.md (copy/paste):

# Day 14 — Networking fundamentals & hands-on checks
## Identity (local machine)
| Command | What it shows |
|--------|----------------|
| **`hostname`** | Server hostname |
| **`hostname -I`** | Main IP address(es) |
| **`ip addr show`** | Interfaces, IPs, netmasks |
| **`ip route`** | Default gateway and routing table |
---
## Reachability (internet / DNS split test)
```bash
ping -c 4 example.com
ping -c 4 8.8.8.8
Interpretation
```

## If 8.8.8.8 works but example.com fails, suspect DNS (name resolution), not basic routing.
## Path (tracepath)
```bash
tracepath dijoker.com
```
### Example output (truncated)

```bash
 1?: [LOCALHOST]                      pmtu 1500
 1:  _gateway                                              1.090ms
 2:  10.56.0.1                                             7.351ms
 ...
10:  no reply
11:  no reply
...
Interpretation
```

### Early hops show your VM → gateway → ISP path with latency.
no reply hops are common on the public internet (many routers block/limit ICMP probes). This does not automatically mean the destination is down.
Listening ports & processes (ss)

```bash
sudo ss -tulpn
```
### Example output
```bash
Netid  State   Recv-Q Send-Q Local Address:Port  Peer Address:Port  Process
tcp    LISTEN  0      128    *:22               *:*                users:(("sshd",pid=1003,fd=3))
tcp    LISTEN  0      128    *:80               *:*                users:(("nginx",pid=1004,fd=8))
tcp    LISTEN  0      128    *:3306             *:*                users:(("mysqld",pid=1005,fd=3))
udp    LISTEN  0      128    *:53               *:*                users:(("systemd-resolve",pid=1006,fd=10))
udp    LISTEN  0      128    *:68               *:*                users:(("systemd-network",pid=1007,fd=10))
udp    LISTEN  0      128    *:5353             *:*                users:(("avahi-daemon",pid=1008,fd=10))
```

### LISTEN means the service is accepting connections on that port.
### UDP entries show DNS-related listeners (*:53, 5353) typical on Ubuntu.
### DNS (dig / nslookup)
### Full query
```bash
dig dijoker.com
```

### Short answer only
```bash
dig dijoker.com +short
```
### OUTPUT:
```bash
172.67.153.239
104.21.12.240
```


### Resolver-style lookup
```bash 
nslookup dijoker.com
Server:		127.0.0.53
Address:	127.0.0.53#53
Non-authoritative answer:
Name:	dijoker.com
Address: 104.21.12.240
Name:	dijoker.com
Address: 172.67.153.239
Name:	dijoker.com
Address: 2606:4700:3033::ac43:99ef
Name:	dijoker.com
Address: 2606:4700:3031::6815:cf0
Interpretation
```

### 127.0.0.53 is Ubuntu’s systemd-resolved stub resolver (common).
### Multiple A/AAAA answers are normal when using Cloudflare-style hosting/CDN.
### HTTP check (curl)
```bash
curl -I dijoker.com
```

```bash
HTTP/1.1 308 Permanent Redirect
...
Location: https://dijoker.com
Server: cloudflare
Interpretation

308 means “redirect permanently” — here it redirects HTTP → HTTPS (Location: https://dijoker.com).
For HTTPS layer checks, follow up with:
curl -I https://dijoker.com
```

### Connections snapshot (netstat vs ss)
### netstat was not installed:

```bash
netstat -an | head
# -bash: netstat: command not found
Use ss instead:

ss -ant | head
Example output

State     Recv-Q Send-Q Local Address:Port    Peer Address:Port Process
LISTEN    0      4096   127.0.0.54:53        0.0.0.0:*
LISTEN    0      70     127.0.0.1:33060      0.0.0.0:*
LISTEN    0      511    0.0.0.0:80           0.0.0.0:*
LISTEN    0      151    127.0.0.1:3306       0.0.0.0:*
LISTEN    0      4096   127.0.0.53%lo:53     0.0.0.0:*
TIME-WAIT 0      0      172.16.165.148:46260 104.21.12.240:80
LISTEN    0      511    [::]:80              [::]:*
LISTEN    0      4096   *:22                 *:*
ESTAB     0      0      [::ffff:172.16.165.148]:22 [::ffff:172.16.165.1]:58781
```