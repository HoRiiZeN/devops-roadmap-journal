# Linux Basics & Command Line

**Started:** Aug 29, 2025  
**Status:** In Progress  
**Estimated completion:** Sept 7, 2025

## Study Log

### Day 1
Learned about Linux history and different distros. Linux has tons of distros and choosing the right one depends on what you want to do (Ubuntu for beginners, CentOS for servers, RHEL for enterprise etc..).

---

### Day 2
Practiced shell navigation cmds (pwd, cd, mkdir, touch, cat, cp, mv, rm). Learned I/O redirection:  
- `>` (overwrite): `echo hello > file.txt`  
- `>>` (append): `echo world >> file.txt`  
- `2>` (errors): `ls /notfound 2> error.txt`  
- `&>` / `&>>` (stdout+stderr): `command &> out.txt` or `command &>> out.txt`  
- `tee` (write + display): `echo hello | tee file.txt`

---
  
### Day 3
Explored Linux variables:
- Local variables (exist only in current shell)
- Environment variables (passed down to child processes)

Common variable commands:
- `echo $VAR` to display values
- `export VAR=value` to create environment variables  
- `env` to list all environment variables

Child shell inheritance test: Variables created in parent shell are available in bash subshells only when exported. Non-exported variables stay inaccessible to child processes.

The `set -o allexport` command automatically exports any new variables.

For permanent settings between sessions:
- `~/.bashrc` for Bash shell users
- `~/.zshrc` for Zsh shell users

---

### Day 4
Explored essential text-processing commands:
- `cut`: Extract sections from lines (-c for chars, -f for fields, -d for delimiter)
- `uniq`: Filter duplicate lines (needs sorted input)
    - `-c`: Show counts
    - `-d`: Show only duplicates
- `paste`: Merge files line by line
- `join`/`split`: Combine or break apart files
- `head`/`tail`: View beginning/end of files
- `expand`/`unexpand`: Convert between tabs and spaces
- `sort`: Order text lines
- `tr`: Translate/replace characters
- `wc`: Count lines/words/characters
- `nl`: Number lines
- `grep`: Search text patterns

Started regex. My head hurt. Will try again later.

Completed [OverTheWire Bandit levels 0-5](https://github.com/HoRiiZeN/overthewire-bandit-notes).

---

### Day 5
Learned a bit about text editors like Vim, but I'm sticking with Nano for now since I'm more comfortable with it. That wrapped up Advanced Text-Fu, and I started the User Management lesson.  

Practiced the basics of users and groups, including the full user lifecycle: creating accounts, securing them, modifying them, and deleting them. Commands used:

- `useradd` : add a new user
- `useradd -m` : add a user and create their home directory
- `sudo` : run commands as superuser/root
- `su user` : switch to another user account :loads their shell:
- `su - user` : switch to another user and load that user's complete environment, including their home directory, PATH variables, and other shell configurations

---

### Day 6
Continued practicing user administration:
- Managed access with `passwd -l` / `passwd -u` (i.e., lock/unlock accounts)
- Managed password aging with `chage` (controls password expiration policies)
- Modified users with `usermod` (e.g., `usermod -aG group user` to add a user to a group)
- Managed groups with `groupadd`
- Checked identities/memberships with `id` and `groups`
- Removed users with:
    - `userdel` (user only)
    - `userdel -r` (user + home dir) *Note: Use with caution as this deletes all user data*

Also, I learned how to:
- Check permissions using the `ls -l` command
- Change file ownership with `chown`
- Modify permissions with `chmod` (using numeric values):
    - `755`: owner has full rights (7 → rwx), group has read/execute (5 → r-x), others also get read/execute (5 → r-x)
    - `750`: would block "others" completely (0 → ---)  

---

### Day 7
Since I haven’t written in this journal until now, I decided to catch up and log Day 1 through Day 6 today."

---

### Day 8
*Yet to come*

---

## Resources Used
- [Linux Journey](https://linuxjourney.com/) - My main Linux learning resource
- [LabEx](https://labex.io/learn) ⭐ – Hands-on labs that reinforced my understanding. *(You get 3 sessions a day, each one is a 60-minute session for free.)*  
- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/) - CTF-style challenges to evaluate my learning <br>

> *⭐ Highly recommended*
## When Complete
**Total days:** : *TBA*  
**Quick thoughts:**  : *TBA*

