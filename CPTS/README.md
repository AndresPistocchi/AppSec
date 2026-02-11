## Enumeration

| Command | Description |
|--------|------------|
| `ps au ` | See logged in users |
| `ls -l ~/.ssh ` | Check for SSH keys for current user |
| `lsblk ` | Check for unmounted file systems/drives |
| `find / -path /proc -prune -o -type d -perm -o+w 2>/dev/null` | Find world-writeable directories (can change perms) |
| `find / -type f \( -name *_hist -o -name *_history \) -exec ls -l {} \; 2>/dev/null` | Find special history files |
| `grep -RniE flag (ask chatgpt)` | Regex command for finding flag in all directories |

## Linux Enumeration
``` bash
ip a   # Check Network Interfaces
w     # who command (checks who is logged in)
history   # checks user's bash history
ls -la /etc/cron.daily/   # check cron jobs
find /proc -name cmdline -exec cat {} \; 2>/dev/null | tr " " "\n" # Look up system information through proc filesystem


