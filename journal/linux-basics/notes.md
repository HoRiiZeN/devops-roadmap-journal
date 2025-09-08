# Linux Basics & Command Line

**Started:** Aug 29, 2025  
**Status:** In Progress  
**Estimated completion:** ~~Sep 7, 2025~~ Sep 8, 2025  
## Study Log

### Day 1
Learned about Linux history and different distros. Linux has tons of distros, and choosing the right one depends on what you want to do (Ubuntu for beginners, CentOS for servers, RHEL for enterprise, etc).

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
- Local variables (exist only in the current shell)
- Environment variables (passed down to child processes)

Common variable commands:
- `echo $VAR` to display values
- `export VAR=value` to create environment variables  
- `env` to list all environment variables

Child shell inheritance test: Variables created in the parent shell are available in bash subshells only when exported. Non-exported variables stay inaccessible to child processes.

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
- Modify permissions with `chmod` (using numeric and symbolic ways):
    - `755`: owner has full rights (7 → rwx), group has read/execute (5 → r-x), others also get read/execute (5 → r-x)
    - `750`: would block "others" completely (0 → ---)  
    - `u+x`: adds execute permission for the user/owner
    - `u-x`: removes execute permission for the user/owner
    - `ug+r`: adds read permission for user and group
---

### Day 7
Since I haven’t written in this journal until now, I decided to catch up and log Day 1 through Day 6 today."

---

### Day 8
Learned about umask (default permission mask for new files and directories) and special permissions:

- SetUID (SUID): allows a program to run with the file owner's privileges (example: `passwd`). Applies only to executable files and is ignored for scripts on most modern systems for security reasons. Set with `chmod u+s file` or `chmod 4755 file`.
- SetGID (SGID): for files, causes execution with the file's group privileges; for directories, new files inherit the directory's group. Set with `chmod g+s file` or `chmod 2755 file`.
- Sticky bit: meaningful only on directories; it ensures that only the file owner or root can remove files inside the directory. Set with `chmod +t dir` or `chmod 1755 dir`.

Finished the permissions section and started processes:

- Basic inspection
    - `ps` shows processes for the current shell
    - `ps aux` lists all system processes with details (USER, PID, %CPU, %MEM)
    - `ps l` shows long format
    - `top` provides a real-time process monitor
- Controlling processes
    - `kill <PID>` sends the default SIGTERM
    - `kill -9 <PID>` sends SIGKILL to force termination (cannot be caught or ignored; no cleanup)
    - Signals:
        - `SIGHUP` (hangup): sent when a controlling terminal closes; daemons often interpret it as "reload config"
        - `SIGINT` (interrupt, Ctrl+C): interactive interrupt; can be caught to perform cleanup before exiting
        - `SIGTERM` (terminate): polite termination request; default for `kill <PID>`; can be caught for graceful shutdown
        - `SIGKILL` (kill, 9): immediate, uncatchable kill; use only when a process won't respond to SIGTERM
        - `SIGSTOP` (stop): pause a process (uncatchable); resume with `SIGCONT`
    - Notes:
        - Prefer `SIGTERM` for normal shutdowns so processes can clean up; use `SIGKILL` as last resort.
        - You can send by name: `kill -SIGTERM <PID>` or by number: `kill -15 <PID>`.
    - Each process has a PID and PPID; init or systemd adopts orphans
    - `_exit` ends a process; parent should `wait` to collect status
    - Orphan: parent dies and process is adopted by init/systemd
    - Zombie: process finished but parent did not `wait`; the process remains as a zombie until the parent collects its exit status with `wait`; if the parent never does, init/systemd will eventually reap the zombie.
- Priority and niceness
    - Start a command with adjusted niceness: `nice -n <value> command`
    - Change a running process priority: `renice <value> <PID>`
- States and internals
    - Common states: R (running), S (sleeping), D (uninterruptible sleep), Z (zombie), T (stopped)
    - `/proc` is a virtual filesystem for process and kernel info, e.g. `/proc/<PID>/status`, `/proc/cpuinfo`
- Job control in the shell
    - Run in background with `&`
    - List jobs with `jobs`
    - Resume in background with `bg`
    - Bring to foreground with `fg`
    - Reference jobs with `%<job>` (example: `kill %1`)

Practiced examples: setting umask, toggling SUID/SGID/sticky bits, inspecting `/proc` entries, killing and renicing processes to reinforce concepts.

---
### Day 9
w.i.p


## Exercises & Projects
See [Exercises](exercises/README.md) for all hands-on practice.

## Resources Used
- [Linux Journey](https://linuxjourney.com/) - My main Linux learning resource
- [LabEx](https://labex.io/learn) ⭐ – Hands-on labs that reinforced my understanding. *(You get 3 sessions a day, each one is a 60-minute session for free. use them wisely)*  
- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/) - CTF-style challenges to evaluate my learning <br>

> *⭐ Highly recommended*

## When Complete
**Total days:** : *TBA*  
**Quick thoughts:**  : *TBA*

