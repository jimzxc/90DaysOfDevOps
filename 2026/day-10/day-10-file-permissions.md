## Day 10 — File permissions and basic file I/O
### Create and append to a file
```bash
touch devops.txt
echo "This is my first line" >> devops.txt
```
### Simple shell script
```bash
nano script.sh
```

### Script contents (shebang must start with #! and use an absolute path to the interpreter):
```bash
#!/bin/bash
touch devops.txt
echo "This is my first line" >> devops.txt
```

### Read file contents
```bash
cat devops.txt
```

### First / last lines of a file
```bash
head -n 10 devops.txt
tail -n 10 devops.txt
```

## Permissions
### Add write + execute for the file:
```bash
chmod +wx devops.txt
(+xw is also valid; order does not matter.)
```

### Numeric mode 755 (owner: rwx, group: r-x, others: r-x) — apply to a file or script:

```bash
chmod 755 script.sh
Run a script (after it is executable)
./script.sh
```


```bash
What I learned to this task is to create filetxt, give permission, execute and write in the script.
```