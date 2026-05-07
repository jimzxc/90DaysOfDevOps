## File I/O practice (Day 06)

## ℹ️ Lessons learned
- I learned how to create a text file.
- I learned how to add content to a text file.
- I learned how to view the beginning and end of a file using `head` and `tail`.
- I learned how to empty a file safely.

---

## Commands practiced

### Create a file
```bash
touch notes.txt
```

### Add content to a file
echo "Line 1" >> notes.txt
echo "Line 2" >> notes.txt
echo "Line 3" | tee -a notes.txt

### View the beginning and end of a file
head -n 2 notes.txt
tail -n 2 notes.txt


### Empty the contents of a file

```bash
> notes.txt
cat /dev/null notes.txt
```