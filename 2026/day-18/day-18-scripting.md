
# Day 18 — Functions & strict mode
## Scripts
- `functions.sh` — greet + add
- `disk_check.sh` — disk + memory checks
- `strict_demo.sh` — tested `set -euo pipefail`
- `local_demo.sh` — local vs global variables
- `system_info.sh` — system info reporter
## Strict mode (`set -euo pipefail`)
- `set -e`: exit on error
- `set -u`: error on unset variables
- `set -o pipefail`: pipeline fails if any command fails
## What I learned (3 key points)
1. Functions make scripts reusable and easier to read.
2. `local` prevents variables from leaking outside functions.
3. Strict mode catches errors early and makes scripts safer.

### Task 1 — functions.sh
```bash
#!/bin/bash
set -euo pipefail
greet() {
  local name="$1"
  printf 'Hello, %s!\n' "$name"
}
add() {
  local a="$1"
  local b="$2"
  printf '%s\n' "$((a + b))"
}
greet "Jimboy"
printf 'Sum: %s\n' "$(add 7 5)"
```

### Task 2 — disk_check.sh (functions + “return values” idea)
#### In bash, functions “return” numbers 0–255 via return, and you output text via echo/printf. Here we print info and return success.

```bash
#!/bin/bash
set -euo pipefail
check_disk() {
  df -h /
}
check_memory() {
  free -h
}
main() {
  printf '%s\n' "=== Disk usage (/) ==="
  check_disk
  printf '\n%s\n' "=== Memory usage ==="
  check_memory
}
main "$@"
```

### Task 3 — strict_demo.sh
#### Uncomment one block at a time to observe the behavior.

```bash
#!/bin/bash
set -euo pipefail
# 1) set -u (unset variable)
# echo "$NOT_SET"
# 2) set -e (command failure)
# false
# echo "You won't see this if false is uncommented"
# 3) pipefail (pipeline failure)
# false | true
# echo "You won't see this if pipefail triggers exit"
printf '%s\n' "Uncomment one test case to see strict mode behavior."
What each flag does (put in your markdown)
set -e → exit the script when a command fails (non‑zero exit)
set -u → exit if you use an unset variable
set -o pipefail → pipeline fails if any command in the pipe fails (not only the last)
```


### Task 4 — local_demo.sh
```bash
#!/bin/bash
set -euo pipefail
value="global"
with_local() {
  local value="local"
  printf 'Inside with_local: %s\n' "$value"
}
without_local() {
  value="changed globally"
  printf 'Inside without_local: %s\n' "$value"
}
printf 'Before: %s\n' "$value"
with_local
printf 'After with_local: %s\n' "$value"
without_local
printf 'After without_local: %s\n' "$value"
```


### Task 5 — system_info.sh (intermediate reporter)

```bash
#!/bin/bash
set -euo pipefail
section() {
  printf '\n%s\n' "===== $1 ====="
}
host_os() {
  section "Hostname & OS"
  hostname
  if [ -r /etc/os-release ]; then
    grep -E '^(PRETTY_NAME)=' /etc/os-release || true
  fi
  uname -a
}
uptime_info() {
  section "Uptime"
  uptime
}
disk_top5() {
  section "Disk usage (top 5 under /)"
  df -h /
  du -xhd1 / 2>/dev/null | sort -hr | head -5 || true
}
memory_info() {
  section "Memory usage"
  free -h
}
top_cpu5() {
  section "Top 5 CPU processes"
  ps aux --sort=-%cpu | head -6
}
main() {
  host_os
  uptime_info
  disk_top5
  memory_info
  top_cpu5
}
main "$@"
```