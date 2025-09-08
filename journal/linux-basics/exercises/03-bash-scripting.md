## **Objective:**  
Write bash script that lists all users, shows disk usage, logs with timestamp

## **Solution:**
I created a file named `cool.sh` and added the following code:
```bash
#!/bin/bash

LOGFILE="log.txt"

echo "Log with timestamp:" >> "$LOGFILE"
date +"%Y-%m-%d %T" >> "$LOGFILE"
echo "---------------------" >> "$LOGFILE"
echo "List of all users:" >> "$LOGFILE"
cut -d: -f1 /etc/passwd  >> "$LOGFILE"
echo "---------------------" >> "$LOGFILE"
echo "Disk usage:" >> "$LOGFILE"
df -h >> "$LOGFILE"
echo "---------------------" >> "$LOGFILE"
echo "log.txt is created successfully..."
```
then I `chmod +x cool.sh` to make it executable and ran it with `./cool.sh`

cool.sh will print a message indicating that `log.txt` is created successfully.
