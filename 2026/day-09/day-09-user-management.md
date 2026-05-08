## Day 09 — User and group management
### Commands practiced
- **`sudo useradd -m <username>`** — create a user and their home directory  
- **`sudo groupadd <groupname>`** — create a group  
- **`sudo usermod -aG <groupname> <username>`** — add a user to a group (append; keeps existing groups)  
- **`chmod 775 <file_or_directory>`** — change permissions (example: group read/write/execute)  
- **`sudo chgrp <groupname> /path/to/file_or_dir`** — change group ownership (often needs `sudo`)  
- **`groups`** — list groups for the **current** user  
- **`groups <username>`** — list groups for a **specific** user  
- **`id <username>`** — show UID, GID, and all groups for that user  
---
## Shell (bash) for a new user
Tab completion and history come from the **shell** (e.g. bash), not from `useradd` alone. Set the login shell when creating the user:
```bash
sudo useradd -m -s /bin/bash <username>
```

## For an existing user:

```bash
sudo chsh -s /bin/bash <username>
```

ℹ️ Lessons learned
```bash
I practiced creating users and groups, adding users to groups, and applying directory permissions.
The main challenge was wiring users → groups → permissions so access behaves as expected.
```