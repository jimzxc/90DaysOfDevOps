# Day 17 — Shell scripting: loops, arguments & error handling

## Task 1 — `for_loop.sh`

Prints five fruits in a `for` loop.

```bash
#!/bin/bash
set -euo pipefail

for fruit in apple banana cherry date elderberry; do
  printf '%s\n' "$fruit"
done
```

---

## Task 1 — `count.sh`

Prints numbers 1–10.

```bash
#!/bin/bash
set -euo pipefail

for i in {1..10}; do
  printf '%s\n' "$i"
done
```

---

## Task 2 — `countdown.sh`

Reads a non-negative integer and counts down to 0, then prints `Done!`.

```bash
#!/bin/bash
set -euo pipefail

read -r -p "Enter a number to count down from: " n

if ! [[ "$n" =~ ^[0-9]+$ ]]; then
  printf '%s\n' "Please enter a non-negative integer." >&2
  exit 1
fi

while [ "$n" -ge 0 ]; do
  printf '%s\n' "$n"
  n=$((n - 1))
done

printf '%s\n' "Done!"
```

---

## Task 3 — `greet.sh`

First argument is the name; prints usage if missing.

```bash
#!/bin/bash
set -euo pipefail

if [ "$#" -lt 1 ]; then
  printf '%s\n' "Usage: $0 <name>" >&2
  exit 1
fi

printf 'Hello, %s!\n' "$1"
```

**Run:** `./greet.sh Alice`

---

## Task 3 — `args_demo.sh`

Shows argument count, all arguments as one string, and script name.

```bash
#!/bin/bash
set -euo pipefail

printf 'Total arguments ($#): %s\n' "$#"
printf 'All arguments ($@): %s\n' "$*"
printf 'Script name ($0): %s\n' "$0"
```

**Note:** `"$*"` joins arguments with the first character of `IFS`. To loop each argument separately, use `"$@"`.

**Run:** `./args_demo.sh a b c`

---

## Task 4 — `install_packages.sh`

Idempotent install for `nginx`, `curl`, and `wget` on Debian/Ubuntu. **Must run as root.**

```bash
#!/bin/bash
set -euo pipefail

if [ "${EUID:-$(id -u)}" -ne 0 ]; then
  printf '%s\n' "Run as root: sudo $0" >&2
  exit 1
fi

packages=(nginx curl wget)

export DEBIAN_FRONTEND=noninteractive
apt-get update -qq

for pkg in "${packages[@]}"; do
  if dpkg -s "$pkg" &>/dev/null; then
    printf '%s: already installed\n' "$pkg"
  else
    apt-get install -y "$pkg"
    printf '%s: installed\n' "$pkg"
  fi
done
```

**Run:** `sudo ./install_packages.sh`

---

## Task 5 — `safe_script.sh`

Uses `set -e` with `||` for a tolerable `mkdir` failure; fails clearly on `cd` or `touch`.

```bash
#!/bin/bash
set -euo pipefail

mkdir /tmp/devops-test 2>/dev/null || printf '%s\n' "Directory already exists (mkdir returned non-zero)."

cd /tmp/devops-test || { printf '%s\n' "Failed to cd into /tmp/devops-test" >&2; exit 1; }

touch devops-note.txt || { printf '%s\n' "Failed to create file" >&2; exit 1; }

printf '%s\n' "Created /tmp/devops-test/devops-note.txt"
```

---

## Run all scripts

```bash
chmod +x for_loop.sh count.sh countdown.sh greet.sh args_demo.sh install_packages.sh safe_script.sh
./for_loop.sh
./count.sh
./greet.sh DevOps
```
