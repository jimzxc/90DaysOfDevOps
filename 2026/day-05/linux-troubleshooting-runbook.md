## Linux troubleshooting runbook (Day 05)

### Target
- **Service**: `ssh` (process: `sshd`)
- **Goal**: capture a quick health snapshot + review logs + list next steps if things worsen

---

## Environment basics
- **`uname -a`**: show kernel + system information
- **`lsb_release -a`**: show Ubuntu distribution/version details
- **`cat /etc/os-release`**: show OS release information (alternative to `lsb_release`)

---

## Filesystem sanity
- **`mkdir -p /tmp/runbook-demo`**: create a throwaway working directory
- **`cp /etc/hosts /tmp/runbook-demo/hosts-copy && ls -larth /tmp/runbook-demo`**: copy a file and verify it exists

---

## Choose the target PID / service
- **`pgrep -a sshd`**: find the `sshd` PID(s) and show the full command line

---

## CPU / memory snapshot
- **`ps -o pid,ppid,user,stat,etime,pcpu,pmem,comm -p <pid>`**: show CPU/memory usage for the selected PID
- **`free -h`**: show memory usage (free vs available)

---

## Disk / I/O snapshot
- **`df -h`**: show filesystem usage (size, used, available)
- **`du -sh /var/log`**: show total size of `/var/log`

---

## Network snapshot
- **`ss -tulpn | head -n 30`**: show listening ports (top portion)
- **`ss -tulpn | grep -i <service>`**: filter listening ports for a service keyword

---

## Logs
- **`journalctl -u <service> -n 50 --no-pager`**: last 50 log lines for the service
- **`journalctl -u <service> -S "today" --no-pager`**: service logs since today
- **`tail -n 50 /var/log/syslog`**: last 50 lines of system log (Ubuntu/Debian)
- **`tail -f <logfile>`**: follow a log file in real time

---

## If this worsens (next steps)
- **`ps aux --sort=-%cpu | head`**: show top CPU-consuming processes
- **`ss -pant`**: show active TCP connections with process info
- **`ss -plant | grep :22`**: show active connections to SSH port 22
- **`sudo lsof -p <pid>`**: list open files/sockets for the process
- **`sudo strace -p <pid> -tt -o /tmp/sshd.strace`**: trace the process briefly (save to a file)


## How I found the `sshd` PID

### List all `sshd` processes
Command:

```bash
pgrep -a sshd



## lesson learned: I learned how to check the process, how many the connectivity of the port. I learned how to check the ubuntu version, details. How to show listening port top portion. Memory and CPU