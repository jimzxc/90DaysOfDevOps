## Day 12 — Revision: commands I rely on

These are commands I use regularly. Together they cover navigation, files, processes, disk, services, logs, users/groups, permissions, networking, and simple automation.

### Navigation & directories
- **`cd`** — change directory  
- **`mkdir`** — create directories  

### Files & text
- **`touch`** — create empty files or update timestamps  
- **`cat`** — print file contents  
- **`head`** — first lines of a file  
- **`tail -n`** — last *n* lines (and **`tail -f`** for live logs)  
- **`echo`** — print text or append to files (`>>`)  

### Processes & resources
- **`htop`** — interactive CPU/memory/process view  
- **`df -h`** — disk space (human-readable)  

### Services & logs (systemd)
- **`systemctl status`** — service state and recent messages  
- **`journalctl -u <service>`** — logs for a unit  

### Users, groups & permissions
- **`adduser`** — interactive user creation (Debian/Ubuntu style)  
- **`addgroup`** — create a group (Debian/Ubuntu; **`groupadd`** on many distros)  
- **`usermod -aG`** — add user to group(s) without removing existing groups  
- **`chown`** — change owner (and optionally group)  
- **`chmod`** — change file permissions  

### Networking
- **`ping`** — basic reachability and latency (example: `ping -c 4 example.com`)
- **`curl`** — HTTP/API checks, downloads
- **`dig`** — DNS lookups
- **`nc` (netcat)** — quick TCP/UDP connectivity tests and simple client/server experiments  
  - Examples: `nc -vz host 443` (TCP port check), `nc -l -p 12345` (listen on a port — lab only)

> **Note:** You wrote **`netcat`** — if you meant **network troubleshooting**, common choices are **`nc`** (netcat), **`ss`**, or **`ping`**. Use **`netcat`** (`nc`) if that’s what you practice.

### Automation
- **`scripts.sh`** — shell scripts (run with **`chmod +x script.sh`** then **`./script.sh`**)

---

## ℹ️ Takeaway
A strong DevOps baseline is not memorizing every flag—it’s knowing **where to look** (disk, processes, services, logs, network, permissions) and having a **small set of commands** you can run fast under pressure.