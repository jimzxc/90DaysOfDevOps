## Day 07 — Linux filesystem notes + troubleshooting scenarios
### Linux directories (quick notes)
- **`/home`**: user home directories (owned by each user)
- **`/`**: root of the filesystem
- **`/root`**: root user’s home directory
- **`/etc`**: system configuration files
- **`/var/log`**: system and application logs
- **`/tmp`**: temporary files (often cleaned automatically)
- **`/bin`**: essential system commands (binaries)
- **`/usr/bin`**: most user-level commands (binaries)
- **`/opt`**: optional / third-party software
### Practice commands
- **Largest items in `/var/log` (top 5)**:
  ```bash
  du -sh /var/log/* 2>/dev/null | sort -h | tail -5
View hostname:
cat /etc/hostname
List home directory (including hidden files):
ls -la ~
Scenarios
1) Service not starting (myapp)
Commands (in order):

systemctl status myapp --no-pager
cat /var/log/myapp.log
systemctl is-enabled myapp
journalctl -u myapp -n 50 --no-pager
2) High CPU usage
htop
ps aux --sort=-%cpu | head -20
3) Finding service logs (systemd example: docker)
systemctl status docker --no-pager
journalctl -u docker -n 50 --no-pager
journalctl -u docker -f
4) Permission denied (/home/user/backup.sh)
ls -l /home/user/backup.sh
chmod +x /home/user/backup.sh
/home/user/backup.sh