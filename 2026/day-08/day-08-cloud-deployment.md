## Day 08 — Cloud/Server Deployment Practice (Vagrant + Docker + Nginx)
### Setup summary
- I’m using **Vagrant** to run a virtual server locally.
- I installed **Docker** manually.
- I installed **Nginx** manually.
---
## System update
```bash
apt update -y
apt upgrade -y
```
## Install and manage Nginx
```bash
apt install nginx
systemctl status nginx
systemctl enable nginx
systemctl start nginx
```

## Check Nginx logs
```bash
cd /var/log/nginx
cat access.log
```

### Sample access.log entries
```bash
192.168.1.9 - - [08/May/2026:15:49:34 +0000] "GET / HTTP/1.1" 200 538 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/147.0.0.0 Safari/537.36"
192.168.1.9 - - [08/May/2026:15:49:36 +0000] "GET /favicon.ico HTTP/1.1" 404 196 "http://192.168.1.10/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/147.0.0.0 Safari/537.36"
192.168.1.9 - - [08/May/2026:15:49:37 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/147.0.0.0 Safari/537.36"
192.168.1.9 - - [08/May/2026:15:49:38 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/147.0.0.0 Safari/537.36"
192.168.1.9 - - [08/May/2026:15:49:39 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/147.0.0.0 Safari/537.36"
192.168.1.9 - - [08/May/2026:15:50:25 +0000] "GET /info.php HTTP/1.1" 200 24645 "http://192.168.1.10/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/147.0.0.0 Safari/537.36"
```