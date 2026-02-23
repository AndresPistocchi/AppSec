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
find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null   # Find binaries with SUID bit set
```

## Word Press
| Command | Description |
|--------|------------|
| ` sudo gem install wpscan ` | Install wpscan |
| ` sudo wpscan --url http://yourVhost --enumerate --api-token INSERT ` | Enumerate and Get API token from WPScan.com |
| ` sudo wpscan --password-attack xmlrpc -t 20 -U user -P /usr/share/wordlists/rockyou.txt --url http://yourVhost ` | Login Bruteforce |



