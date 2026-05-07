## Linux practice (Day 04)

### Process checks
- **`ps aux | head`**: show the first few running processes
- **`top`** (or **`htop`**): live view of CPU/memory usage per process
- **`pgrep -a ssh`**: list matching processes with full command line
- **`ps -p <pid>`**: show details for a specific process ID

### Service checks
- **`systemctl status <service> --no-pager`**: check service status and recent logs
- **`systemctl list-units --type=service --state=running`**: list running services
- **`systemctl cat <service>`**: view the service unit file

### Log checks
- **`journalctl -u <service> -n 50 --no-pager`**: show last 50 log lines for a service
- **`journalctl -u <service> -S "today" --no-pager`**: show service logs since today
- **`tail -n 50 /var/log/syslog`**: show last 50 lines of system log (Debian/Ubuntu)