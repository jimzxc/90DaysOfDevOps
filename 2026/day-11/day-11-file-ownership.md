## Day 11 — File ownership
### Workflow
1. **`ls -la`** — list files and directories in the current location (includes owner, group, and permissions).
2. Review **ownership** (user and group) in the listing.
3. Change ownership or group as needed (see commands below).
4. **`ls -la`** again to verify.
5. **`ls -lR`** — recursive listing (files and subdirectories under the current path).
---
### Change owner and group
```bash
sudo chown owner:group /path/to/file_or_directory
```


### Change group only
```bash 
sudo chgrp newgroup /path/to/filename
```

### Using chown to set group only (leave owner unchanged):

```bash
sudo chown :newgroup /path/to/filename
```

### Recursive changes (directory trees)
```bash
sudo chown -R owner:group /path/to/directory
```

ℹ️ Notes
```bash
chown and chgrp usually need sudo when the objects are not owned by your user.
Syntax is user:group for chown; use :group if you only want to change the group.
```