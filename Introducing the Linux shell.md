# General usage commands 
**1- echo $0**  to show the used shell

**2- /etc/passwd** file contains lines  for each user. for each user a shell is defined. 

3- to show available shells : **cat /etc/shells**

4- to change betwwen virtual terminals use **chvt N** 

5- **who** command gives info on logged users and their tty

# Linux Process Management Commands Cheat Sheet

## 📊 **Process Monitoring & Information**

| Command | Description | Common Options | Example |
|---------|-------------|----------------|---------|
| **`ps`** | Display running processes | `-e` (all), `-f` (full), `-u user`, `--forest` (tree) | `ps -ef \| grep python` |
| **`top`** | Interactive process viewer | `-d delay`, `-p PID`, `-u user`, `-c` (cmdline) | `top -u apache` |
| **`htop`** | Enhanced interactive viewer | `-u user`, `-p PID`, `-t` (tree) | `htop` |
| **`pstree`** | Show process tree | `-p` (PIDs), `-u` (users), `-a` (args) | `pstree -paul` |
| **`pgrep`** | Find PIDs by name | `-l` (list names), `-u user`, `-f` (full match) | `pgrep -f nginx` |
| **`pidof`** | Get PID of running program | `-s` (single), `-x` (exact) | `pidof sshd` |

## 🎯 **Process Control & Signals**

| Command | Description | Common Signals | Example |
|---------|-------------|----------------|---------|
| **`kill`** | Send signal to process | `-9` (KILL), `-15` (TERM), `-1` (HUP) | `kill -9 1234` |
| **`pkill`** | Kill by process name | `-9` (force), `-f` (full), `-u user` | `pkill -9 firefox` |
| **`killall`** | Kill all processes by name | `-9` (force), `-u user`, `-v` (verbose) | `killall -u bob` |
| **`skill`** | Send signal (legacy) | `-9`, `-KILL`, `-STOP` | `skill -KILL -u alice` |
| **`renice`** | Change process priority | `-n value`, `-p PID`, `-u user` | `renice +5 1234` |
| **`nohup`** | Run immune to hangups | (none) | `nohup ./script.sh &` |

## 🔄 **Background & Job Control**

| Command | Description | Usage | Example |
|---------|-------------|-------|---------|
| **`&`** | Run in background | `command &` | `sleep 100 &` |
| **`jobs`** | List background jobs | `-l` (with PIDs), `-p` (PIDs only) | `jobs -l` |
| **`fg`** | Bring to foreground | `%jobid` or `%` (current) | `fg %1` |
| **`bg`** | Resume in background | `%jobid` or `%` (current) | `bg %2` |
| **`disown`** | Remove from job table | `-h` (keep in jobs), `-a` (all) | `disown %1` |
| **`wait`** | Wait for process completion | `PID` or `%jobid` | `wait 1234` |

## 📈 **Performance & Resources**

| Command | Description | Key Options | Example |
|---------|-------------|-------------|---------|
| **`uptime`** | System load & uptime | (none) | `uptime` |
| **`free`** | Memory usage | `-h` (human), `-m` (MB), `-s sec` | `free -h` |
| **`vmstat`** | Virtual memory stats | `-s` (summary), `delay count` | `vmstat 2 5` |
| **`iostat`** | CPU & I/O statistics | `-c` (CPU), `-d` (device), `-x` (extended) | `iostat -dx 2` |
| **`mpstat`** | CPU statistics | `-P ALL` (all CPUs), `interval` | `mpstat -P ALL 2` |
| **`sar`** | System activity report | `-u` (CPU), `-r` (memory), `-b` (I/O) | `sar -u 2 5` |

## 🔍 **Process Details & Debugging**

| Command | Description | Useful Options | Example |
|---------|-------------|----------------|---------|
| **`lsof`** | List open files | `-p PID`, `-u user`, `-i` (network), `-c name` | `lsof -p 1234` |
| **`strace`** | Trace system calls | `-p PID`, `-f` (follow forks), `-e trace=file` | `strace -p 5678` |
| **`ltrace`** | Trace library calls | `-p PID`, `-f` (follow forks) | `ltrace -p 5678` |
| **`time`** | Time command execution | `-p` (POSIX), `-v` (verbose) | `time ls -R /` |
| **`/proc/`** | Process info filesystem | (directory) | `cat /proc/1234/status` |

## 🚀 **Process Startup & Priority**

| Command | Description | Important Options | Example |
|---------|-------------|-------------------|---------|
| **`nice`** | Run with modified priority | `-n value`, command | `nice -n 10 tar -czf backup.tar.gz /data` |
| **`taskset`** | Set CPU affinity | `-c` (CPU list), `-p` (PID) | `taskset -c 0,2 ./app` |
| **`chrt`** | Change real-time attributes | `-f` (FIFO), `-r` (RR), `-p` (PID) | `chrt -f -p 99 1234` |
| **`ionice`** | Set I/O priority | `-c class`, `-n level`, `-p PID` | `ionice -c2 -n7 ./backup.sh` |

## 📊 **System Monitoring Tools**

| Command | Description | When to Use | Example |
|---------|-------------|-------------|---------|
| **`glances`** | Comprehensive monitor | Real-time monitoring | `glances` |
| **`bpytop`** | Python-based resource monitor | Modern alternative to top | `bpytop` |
| **`nmon`** | Nigel's performance monitor | Performance analysis | `nmon` |
| **`dstat`** | Versatile resource stats | Customizable metrics | `dstat -cdngy` |
| **`atop`** | Advanced process monitor | Historical process analysis | `atop` |

## 🛠️ **Special Process Operations**

| Command | Description | Use Case | Example |
|---------|-------------|----------|---------|
| **`screen`** | Terminal multiplexer | Long-running processes | `screen -S session` |
| **`tmux`** | Terminal multiplexer | Modern alternative to screen | `tmux new -s mysession` |
| **`setsid`** | Run in new session | Detach from terminal | `setsid ./daemon.sh` |
| **`timeout`** | Run with time limit | Prevent hanging commands | `timeout 10s ./script.sh` |
| **`cgroups`** | Control groups | Resource limiting | `cgcreate -g cpu,memory:/mygroup` |

## 📋 **Process Information Files**

| File | Contains | Useful Commands |
|------|----------|-----------------|
| **`/proc/[PID]/status`** | Process status | `cat /proc/$$/status` |
| **`/proc/[PID]/cmdline`** | Command line | `cat /proc/$$/cmdline \| xargs -0 echo` |
| **`/proc/[PID]/fd/`** | Open file descriptors | `ls -la /proc/$$/fd/` |
| **`/proc/[PID]/environ`** | Environment variables | `cat /proc/$$/environ \| tr '\0' '\n'` |
| **`/proc/loadavg`** | System load average | `cat /proc/loadavg` |
| **`/proc/meminfo`** | Memory information | `cat /proc/meminfo` |

## 🎮 **Interactive Shortcuts (Bash)**

| Shortcut | Action | Description |
|----------|--------|-------------|
| **`Ctrl+C`** | SIGINT | Interrupt/kill foreground process |
| **`Ctrl+Z`** | SIGTSTP | Suspend foreground process |
| **`Ctrl+\`** | SIGQUIT | Quit with core dump |
| **`Ctrl+D`** | EOF | End of file/exit shell |
| **`Ctrl+S`** | (none) | Pause terminal output |
| **`Ctrl+Q`** | (none) | Resume terminal output |
| **`Ctrl+L`** | (none) | Clear screen |

## 📝 **Useful One-Liners**

```bash
# Find and kill zombie processes
ps aux | awk '{if ($8=="Z") print $2}' | xargs kill -9

# Monitor specific process memory
watch -n1 'ps -p PID -o pid,ppid,cmd,%mem,%cpu,state'

# Show process tree with resource usage
ps axuf --forest

# Kill all processes older than 1 hour
ps -eo pid,etime,comm | awk '$2~/^[0-9]+:[0-9]+:[0-9]+/ {print $1}' | xargs kill

# Monitor file opens by process
strace -f -e trace=open,openat,close,read,write -p PID 2>&1 | grep -v ENOENT
```

## 🔧 **Systemd Process Management**

| Command | Description | Equivalent SysVinit |
|---------|-------------|---------------------|
| **`systemctl start service`** | Start service | `service service start` |
| **`systemctl stop service`** | Stop service | `service service stop` |
| **`systemctl restart service`** | Restart service | `service service restart` |
| **`systemctl status service`** | Check status | `service service status` |
| **`systemctl enable service`** | Enable at boot | `chkconfig service on` |
| **`systemctl disable service`** | Disable at boot | `chkconfig service off` |
| **`journalctl -u service`** | View logs | `tail -f /var/log/service.log` |

---

## 📌 **Quick Reference: Signal Numbers**

| Signal | Number | Description | Default Action |
|--------|--------|-------------|----------------|
| **SIGHUP** | 1 | Hangup detected | Terminate |
| **SIGINT** | 2 | Interrupt (Ctrl+C) | Terminate |
| **SIGQUIT** | 3 | Quit (Ctrl+\) | Terminate + Core |
| **SIGKILL** | 9 | Kill (cannot be caught) | Terminate |
| **SIGTERM** | 15 | Termination (polite) | Terminate |
| **SIGSTOP** | 19 | Stop (cannot be caught) | Stop process |
| **SIGTSTP** | 20 | Terminal stop (Ctrl+Z) | Stop process |
| **SIGCONT** | 18 | Continue | Continue if stopped |

---

## 💡 **Pro Tips**

1. **Use `kill -TERM` before `kill -KILL`** - Give processes chance to cleanup
2. **Check `/proc/PID/status`** for detailed process state
3. **Combine commands**: `ps auxf | less` or `watch -n1 'ps aux --sort=-%cpu | head -20'`
4. **Use `htop`** for interactive process management (F9 for kill menu)
5. **Remember `$!`** stores PID of last background process
6. **Monitor with `pidstat`**: Comprehensive per-process stats
7. **Use `cgroups`** for advanced resource control in production

---

# Linux User, Group & Permission Management Cheat Sheet

## 👤 **User Management**

### **User Information & Status**

| Command | Description | Common Options | Example |
|---------|-------------|----------------|---------|
| **`whoami`** | Current username | (none) | `whoami` |
| **`id`** | User/group IDs | `-u` (UID), `-g` (GID), `-n` (names), `-a` (all) | `id -un` |
| **`who`** | Logged in users | `-b` (boot time), `-H` (headers), `-q` (count) | `who -H` |
| **`w`** | Who & what they're doing | `-h` (no header), `-u` (ignore username), `-f` (from) | `w -h` |
| **`last`** | Last logged in users | `-a` (host), `-d` (DNS), `-x` (shutdowns), `-n X` (limit) | `last -n 5` |
| **`users`** | Compact logged in list | (none) | `users` |
| **`finger`** | User information | `-l` (long), `-s` (short), `-p` (no .plan) | `finger user` |
| **`logname`** | Login name | (none) | `logname` |

### **User Creation & Modification**

| Command | Description | Key Options | Example |
|---------|-------------|-------------|---------|
| **`useradd`** | Add new user | `-m` (home), `-s shell`, `-g group`, `-G groups`, `-u UID`, `-c comment` | `useradd -m -s /bin/bash john` |
| **`adduser`** | Interactive add (Debian) | `--system`, `--home DIR`, `--shell SHELL`, `--ingroup GROUP` | `adduser --system backup` |
| **`usermod`** | Modify user | `-L` (lock), `-U` (unlock), `-aG` (add groups), `-s` (shell), `-d` (home) | `usermod -aG sudo john` |
| **`userdel`** | Delete user | `-r` (remove home), `-f` (force) | `userdel -r john` |
| **`passwd`** | Change password | `-l` (lock), `-u` (unlock), `-d` (delete), `-e` (expire), `-S` (status) | `passwd john` |
| **`chsh`** | Change shell | `-l` (list shells), `-s shell` | `chsh -s /bin/zsh` |
| **`chfn`** | Change finger info | `-f name`, `-h home`, `-p phone`, `-o office` | `chfn -f "John Doe"` |

### **User Session Management**

| Command | Description | Usage | Example |
|---------|-------------|-------|---------|
| **`su`** | Switch user | `-` (login shell), `-c command`, `-s shell` | `su - john` |
| **`sudo`** | Execute as superuser | `-u user`, `-i` (login), `-l` (list), `-k` (reset) | `sudo -u mysql ls` |
| **`newgrp`** | Switch primary group | `groupname` | `newgrp developers` |
| **`logout`** | End login session | (none) | `logout` |
| **`exit`** | Exit shell/session | (none) | `exit` |

### **User Configuration Files**

| File | Purpose | Format |
|------|---------|--------|
| **`/etc/passwd`** | User accounts | `username:x:UID:GID:comment:homedir:shell` |
| **`/etc/shadow`** | Encrypted passwords | `username:password:lastchg:min:max:warn:inactive:expire:reserved` |
| **`/etc/login.defs`** | Default user values | Key-value pairs |
| **`/etc/default/useradd`** | useradd defaults | Configuration variables |
| **`~/.profile`** | User startup script | Shell commands |
| **`~/.bashrc`** | Bash config | Aliases, functions |

---

## 👥 **Group Management**

### **Group Information**

| Command | Description | Options | Example |
|---------|-------------|---------|---------|
| **`groups`** | User's groups | `username` | `groups john` |
| **`getent`** | Get group entry | `group groupname` | `getent group sudo` |
| **`lid`** | List group members | `-g groupname`, `-d` (delete) | `lid -g sudo` |

### **Group Creation & Modification**

| Command | Description | Key Options | Example |
|---------|-------------|-------------|---------|
| **`groupadd`** | Create group | `-g GID`, `-r` (system), `-o` (non-unique) | `groupadd -g 1001 developers` |
| **`groupmod`** | Modify group | `-n newname`, `-g newGID` | `groupmod -n devs developers` |
| **`groupdel`** | Delete group | (none) | `groupdel testgroup` |
| **`gpasswd`** | Group admin | `-a user`, `-d user`, `-M users`, `-A admins`, `-R` (restrict) | `gpasswd -a john sudo` |

### **Group Configuration Files**

| File | Purpose | Format |
|------|---------|--------|
| **`/etc/group`** | Group definitions | `groupname:x:GID:members` |
| **`/etc/gshadow`** | Secure group data | `groupname:encrypted:admins:members` |

---

## 🔐 **Permission Management**

### **Basic Permission Commands**

| Command | Description | Syntax | Example |
|---------|-------------|--------|---------|
| **`chmod`** | Change mode | Symbolic: `ugoa+-=rwx`, Octal: `0-7` | `chmod 755 file`, `chmod u+x script.sh` |
| **`chown`** | Change owner | `owner:group`, `owner.group` | `chown john:devs file` |
| **`chgrp`** | Change group | `groupname` | `chgrp www-data /var/www` |
| **`umask`** | Set default permissions | Octal mask | `umask 022` |
| **`getfacl`** | Get ACLs | `-a` (access), `-d` (default) | `getfacl file` |
| **`setfacl`** | Set ACLs | `-m` (modify), `-x` (remove), `-b` (remove all) | `setfacl -m u:john:rw file` |

### **Special Permission Bits**

| Bit | Symbol | Octal | Effect | Example |
|-----|--------|-------|--------|---------|
| **SetUID** | `s` or `S` | 4000 | Run as owner | `chmod u+s /usr/bin/passwd` |
| **SetGID** | `s` or `S` | 2000 | Run as group, dirs: inherit group | `chmod g+s /shared` |
| **Sticky** | `t` or `T` | 1000 | Only owner can delete in dir | `chmod +t /tmp` |

### **Permission Checking**

| Command | Description | Useful for | Example |
|---------|-------------|------------|---------|
| **`ls -l`** | List with permissions | Quick view | `ls -la /home` |
| **`stat`** | File status | Detailed info | `stat -c "%a %n" file` |
| **`find -perm`** | Find by permissions | Security audit | `find / -perm -4000 2>/dev/null` |
| **`namei`** | Follow symlinks | Permission path | `namei -l /usr/bin/python` |

---

## 🛡️ **Security & Access Control**

### **PAM (Pluggable Authentication Modules)**

| File/Dir | Purpose | Location |
|----------|---------|----------|
| **`/etc/pam.d/`** | PAM config files | Service-specific |
| **`pam_tally2`** | Failed login counter | `pam_tally2 -u john` |
| **`faillock`** | Lock after fails | `faillock --user john` |

### **SUDO Configuration**

| Command | Description | Usage |
|---------|-------------|-------|
| **`visudo`** | Edit sudoers safely | `visudo` |
| **`sudo -l`** | List allowed commands | `sudo -l` |
| **Sudoers Syntax** | Grant privileges | `john ALL=(ALL) NOPASSWD: /usr/bin/apt` |

### **Account Limits**

| Command | Description | Configuration File |
|---------|-------------|-------------------|
| **`ulimit`** | Shell limits | `ulimit -a` |
| **`pam_limits`** | System limits | `/etc/security/limits.conf` |
| **`systemd`** | Service limits | `.service` files |

---

## 📊 **Audit & Monitoring**

### **User Activity Monitoring**

| Command | Description | Options | Example |
|---------|-------------|---------|---------|
| **`lastlog`** | Last login times | `-u user`, `-t days`, `-b days` | `lastlog -t 7` |
| **`faillog`** | Failed login log | `-u user`, `-a` (all), `-r` (reset) | `faillog -u john` |
| **`ac`** | Connect time stats | `-d` (daily), `-p` (per user), `-a` (all) | `ac -d` |
| **`lastb`** | Failed login attempts | (none) | `lastb` |
| **`who -b`** | Last system boot | (none) | `who -b` |

### **Security Scanning**

| Command | Description | Purpose | Example |
|---------|-------------|---------|---------|
| **`find / -nouser`** | Orphaned files | Security audit | `find / -nouser -o -nogroup 2>/dev/null` |
| **`find / -perm -o=w`** | World-writable | Security check | `find / -perm -o=w ! -type l 2>/dev/null` |
| **`find / -perm -4000`** | SetUID files | Privilege escalation check | `find / -type f -perm -4000 2>/dev/null` |
| **`lsof -i`** | Open network connections | Network audit | `lsof -i :80` |

---

## 📝 **File Permission Examples**

### **Common Permission Scenarios**

| Scenario | Symbolic | Octal | Command |
|----------|----------|-------|---------|
| **Secure directory** | `rwx------` | 700 | `chmod 700 ~/private` |
| **Shared directory** | `rwxrwx---` | 770 | `chmod 770 /shared` |
| **Web directory** | `rwxr-xr-x` | 755 | `chmod 755 /var/www` |
| **Read-only config** | `r--r-----` | 440 | `chmod 440 /etc/config` |
| **Executable script** | `rwxr-xr-x` | 755 | `chmod 755 script.sh` |
| **Log file** | `rw-r-----` | 640 | `chmod 640 /var/log/app.log` |

### **Special Permissions**

| Use Case | Command | Effect |
|----------|---------|--------|
| **SUID binary** | `chmod 4755 /usr/bin/program` | Runs as owner |
| **SGID directory** | `chmod 2775 /shared` | New files inherit group |
| **Sticky temp dir** | `chmod 1777 /tmp` | Only owners can delete |
| **All three** | `chmod 7777 file` | SUID+SGID+Sticky |

---

## 🔧 **Advanced Features**

### **ACL (Access Control Lists)**

| Command | Description | Example |
|---------|-------------|---------|
| **Add user ACL** | `setfacl -m u:username:permissions file` | `setfacl -m u:john:rwx file` |
| **Add group ACL** | `setfacl -m g:groupname:permissions file` | `setfacl -m g:devs:rw file` |
| **Default ACLs** | `setfacl -d -m u:username:perms dir` | `setfacl -d -m u:john:rwx /shared` |
| **Remove ACL** | `setfacl -x u:username file` | `setfacl -x u:john file` |
| **Copy ACL** | `getfacl file1 \| setfacl --set-file=- file2` | Copy ACL between files |

### **Extended Attributes**

| Command | Description | Example |
|---------|-------------|---------|
| **`lsattr`** | List attributes | `lsattr file` |
| **`chattr`** | Change attributes | `chattr +i file` (immutable) |
| Common Attributes: `i` (immutable), `a` (append-only), `A` (no atime) |

### **Capabilities (Linux Capabilities)**

| Command | Description | Example |
|---------|-------------|---------|
| **`getcap`** | Get capabilities | `getcap /usr/bin/ping` |
| **`setcap`** | Set capabilities | `setcap cap_net_raw+ep /usr/bin/ping` |

---

## 📋 **Quick Reference Tables**

### **Octal Permission Table**

| Octal | Binary | Permissions | Readable |
|-------|--------|-------------|----------|
| 0 | 000 | `---` | No access |
| 1 | 001 | `--x` | Execute only |
| 2 | 010 | `-w-` | Write only |
| 3 | 011 | `-wx` | Write + Execute |
| 4 | 100 | `r--` | Read only |
| 5 | 101 | `r-x` | Read + Execute |
| 6 | 110 | `rw-` | Read + Write |
| 7 | 111 | `rwx` | Read + Write + Execute |

### **User/Group ID Ranges**

| Range | Type | Typical Use |
|-------|------|-------------|
| 0 | root | Superuser |
| 1-999 | System | Daemons, services |
| 1000-60000 | Regular | Human users |
| 65534 | nobody | Unprivileged |

### **Default umask Values**

| umask | Files | Directories | Use Case |
|-------|-------|-------------|----------|
| 022 | 644 (`rw-r--r--`) | 755 (`rwxr-xr-x`) | Standard |
| 027 | 640 (`rw-r-----`) | 750 (`rwxr-x---`) | Secure |
| 077 | 600 (`rw-------`) | 700 (`rwx------`) | Private |
| 000 | 666 (`rw-rw-rw-`) | 777 (`rwxrwxrwx`) | Open |

---

## 🚀 **Useful One-Liners**

### **User Management**
```bash
# List all users with UID >= 1000 (regular users)
getent passwd | awk -F: '$3 >= 1000 && $3 < 60000 {print $1}'

# Find users without password
sudo awk -F: '($2 == "") {print $1}' /etc/shadow

# List users in sudo group
getent group sudo | cut -d: -f4 | tr ',' '\n'

# Show user login history
last -f /var/log/wtmp | grep "^username"

# Count failed logins per user
sudo lastb | awk '{print $1}' | sort | uniq -c | sort -nr
```

### **Permission Management**
```bash
# Find world-writable files
find / -xdev -type f -perm -o=w ! -type l 2>/dev/null

# Find SUID/SGID files
find / -xdev -type f \( -perm -4000 -o -perm -2000 \) 2>/dev/null

# Fix directory permissions recursively
find /path -type d -exec chmod 755 {} \;
find /path -type f -exec chmod 644 {} \;

# Backup and restore permissions
getfacl -R /path > permissions.acl
setfacl --restore=permissions.acl

# List files owned by user
find / -user username 2>/dev/null | head -20
```

### **Security Audits**
```bash
# Check for empty passwords
sudo awk -F: '($2 == "" || $2 == "!") {print $1}' /etc/shadow

# Find .ssh directories with wrong permissions
find /home -type d -name .ssh -exec ls -ld {} \; | awk '$1 !~ /drwx------/'

# Check for suspicious crontabs
sudo ls -la /var/spool/cron/crontabs/

# Audit sudo access
sudo -l | grep -E "(ALL|NOPASSWD)"
```

---

## 🛠️ **Systemd Integration**

| Command | Description | Example |
|---------|-------------|---------|
| **`loginctl`** | Session management | `loginctl list-sessions` |
| **`systemd-run`** | Run as user | `systemd-run --user --scope command` |
| **`machinectl`** | Container users | `machinectl shell user@container` |

---

## 📁 **Important Configuration Files**

| File | Purpose | Key Settings |
|------|---------|--------------|
| **`/etc/passwd`** | User database | UID, GID, shell, home |
| **`/etc/shadow`** | Password hashes | Password aging, locks |
| **`/etc/group`** | Group database | Group memberships |
| **`/etc/sudoers`** | Sudo permissions | Command aliases, NOPASSWD |
| **`/etc/login.defs`** | Login defaults | UID/GID ranges, passwords |
| **`/etc/security/limits.conf`** | Resource limits | nofile, nproc, etc. |
| **`/etc/pam.d/`** | Authentication | Password policies, MFA |

---

## 💡 **Best Practices**

1. **Principle of Least Privilege**: Grant minimum necessary permissions
2. **Use groups** for shared access, not world permissions
3. **Regular audits**: Check for orphaned files, wrong permissions
4. **Password policies**: Enforce complexity, expiration
5. **SUID/SGID minimization**: Remove unnecessary setuid binaries
6. **ACL over groups**: For complex permission scenarios
7. **sudo over su**: Better auditing, control
8. **Separate service accounts**: Don't run services as root
9. **Monitor /etc/passwd changes**: `inotifywait -m /etc/passwd`
10. **Use SSH keys** over passwords when possible

---

## ⚠️ **Common Pitfalls**

1. **`chmod -R 777 /`** - NEVER DO THIS!
2. **World-writable home directories** - Security risk
3. **SUID shell scripts** - Major security vulnerability
4. **Password in /etc/passwd** - Use shadow file
5. **Root SSH login** - Disable in sshd_config
6. **Shared accounts** - Individual accounts only
7. **Weak sudo configurations** - Be specific with commands

---
