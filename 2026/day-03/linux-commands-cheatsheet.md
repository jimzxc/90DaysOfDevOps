## 20 commands that I practiced
### File system + text
- **`pwd`**: print current directory
- **`ls -lah`**: list files (including hidden) in long format with human-readable sizes
- **`cd /path`**: change directory
- **`mkdir -p dir/subdir`**: create directories (including parent dirs if missing)
- **`cp -a src/ dest/`**: copy while preserving attributes
- **`mv old new`**: move/rename files or directories
- **`rm -r path`**: remove directories/files recursively (be careful)
- **`cat filename`**: print file contents
- **`less file`**: page through a file (search with `/`)
- **`head -n 50 file`**: show first 50 lines
- **`tail -n 50 file`**: show last 50 lines
- **`tail -f file`**: follow logs in real time
- **`grep -n "pattern" file`**: search text with line numbers
### Process management
- **`ps aux`**: snapshot of running processes
- **`top`** (or **`htop`**): live process/CPU/memory view
- **`kill -TERM <pid>`**: gracefully stop a process
- **`kill -9 <pid>`**: force kill (last resort)
- **`systemctl status <service>`**: check service status (systemd)
- **`journalctl -u <service> -e`**: view service logs (systemd)
### Networking
- **`ping -c 4 <host>`**: basic reachability/latency test
- **`ip addr`**: view IP addresses/interfaces (Linux)
- **`ss -tulpn`**: show listening ports and owning processes
- **`curl -I https://example.com`**: check HTTP response headers
- **`dig example.com`**: DNS lookup