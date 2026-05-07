## 20 commands that I practiced.

## File system + text

``` pwd: to print current directory
ls -lah: list files together with hidden files
cd /path: change directory
mkdir -p dir/subdir: create directory or folder
cp -a src/ dest/: copy while preserving attributes
mv old new: renaming directory
rm -r path: remove directories/files recursively
cat filename: print file contents
less file: page through a file (search with /)
head -n 50 file: first 50 lines
tail -n 50 files: last 50 lines
tail -f file: follow logs in real time
grep -n "pattern" file: search text with line numbers ```

## Process management
``` ps aux: snapshot of running processes
top or (htop): live process/CPU/mem view
kill -TERM <pid>: gracefully stop the process
kill -9 <pid>: force kill
systemctl status <service>: to check the status of the service (sytemd)
journalctl -u <service> -e: view service logs (systemd) ```

## Networking
``` ping -c 4 <host/URL>: basic reachability/latency test
ip addr: view ip addresses/interfaces (Linux)
ss -tulpn: show listening ports and owning processes
curl -I https://example.com: check the http response headers
dig example.com: DNS lookup ```