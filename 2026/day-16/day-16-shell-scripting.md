# Day 16 — Shell scripting notes
## Hello world (`hello.sh`)
```bash
#!/bin/bash
echo "Hello, World Class DevOps!"
```
- Shebang (#!/bin/bash)
If you remove the shebang, the script can still run when executed as ./hello.sh because the kernel may fall back to default behavior, or you invoke it with bash hello.sh. Best practice: keep a shebang so the script always runs with the intended interpreter.



### Variables (variables.sh)
```bash
#!/bin/bash
NAME="Jimboy Balan"
ROLE="DevOps Engineer"
echo "I am ${NAME} and I am a ${ROLE}"
```
- Quote style: use double quotes so variables expand; use single quotes for literal text. Prefer "${NAME}" over broken quoting like "I am "$NAME"".


### User input (read)
```bash
#!/bin/bash
echo "Can you put down your Full Name?"
read -r name
echo "Your full name is ${name}"
If / else — number check (check_number.sh)
#!/usr/bin/env bash
set -euo pipefail
read -r -p "Enter a number: " num
if ! [[ "$num" =~ ^-?[0-9]+$ ]]; then
  printf '%s\n' "Please enter a valid integer." >&2
  exit 1
fi
if [ "$num" -gt 0 ]; then
  printf '%s\n' "The number is positive."
elif [ "$num" -lt 0 ]; then
  printf '%s\n' "The number is negative."
else
  printf '%s\n' "The number is zero."
fi
Service check (server_check.sh)
#!/usr/bin/env bash
set -euo pipefail
# Default service; override: SERVICE=ssh ./server_check.sh
SERVICE="${SERVICE:-nginx}"
read -r -p "Do you want to check the status? (y/n) " answer
case "${answer,,}" in
  y|yes)
    systemctl status "$SERVICE" --no-pager || true
    if systemctl is-active --quiet "$SERVICE"; then
      printf '%s\n' "Service '$SERVICE' is active."
    else
      printf '%s\n' "Service '$SERVICE' is not active."
    fi
    ;;
  n|no)
    printf '%s\n' "Skipped."
    ;;
  *)
    printf '%s\n' "Please answer y or n." >&2
    exit 1
    ;;
esac
```

### Note: On Ubuntu, SSH is often unit ssh, not sshd. Example: SERVICE=ssh ./server_check.sh.

## Run scripts
```bash
chmod +x hello.sh variables.sh check_number.sh server_check.sh
./hello.sh
```