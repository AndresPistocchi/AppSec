## Enumeration

| Command | Description |
|--------|------------|
| `ps au ` | See logged in users |
| `ls -l ~/.ssh ` | Check for SSH keys for current user |
| `lsblk ` | Check for unmounted file systems/drives |
| `find / -path /proc -prune -o -type d -perm -o+w 2>/dev/null` | Find world-writeable directories (can change perms) |
