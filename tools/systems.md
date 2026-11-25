# Systems tool

## btop
A resource monitor that shows information about the CPU, memory, disks, network and processes.

```bash
btop

# In-session keys: m = menu, f = filter processes, +/- = favorites,
# h = help, q = quit
```

## lsof
List open files and the corresponding processes.

```bash
# List open ports by process and PID with no-resolution
sudo lsof -i -P -n

# Which process holds a port?
sudo lsof -i :443

# Only listening TCP sockets
sudo lsof -i -P -n -sTCP:LISTEN

# Files opened by a given process
sudo lsof -p <pid>

# Which process has a file/directory open (e.g. before unmounting)
sudo lsof +D /mnt/data
lsof /var/log/syslog

# Deleted files still held open (space not freed yet)
sudo lsof +L1
```

## ncdu
Disk usage analyzer with an ncurses interface.

```bash
ncdu

# Analyze a specific path
ncdu /var/log

# Export results to read later / on another machine
ncdu -o scan.json /
ncdu -f scan.json

# In-session keys: enter = descend, d = delete, c = calculate shares,
# q = quit
```
## ufw
Uncomplicated Firewall

```bash
# Run as sudo

# Check status (enabled/disabled)
ufw status

# Enable / Disable
ufw enable
ufw disable

# Add rule and comment
ufw allow ssh comment "Allow SSH"

# specific incoming interface
ufw allow in on enp0s2 proto tcp port 22 comment "Allow SSH"

# specific source ip
ufw allow from 192.168.1.0/24 proto tcp to 192.168.0.1 port 22 comment "Allow SSH"

# Print rules numbered
ufw status numbered

# Delete by number
ufw delete 8

# Recommended default mode
ufw default reject incoming
ufw default allow outgoing
ufw default deny routed

# Enable loggin
ufw logging on
```
Remember to check the logs, for example from dmesg, and comment on all added rules.

## fail2ban
Blocks repeated offenders (mainly brute-force auth attempts) by watching logs and injecting firewall rules.

```bash
# Overall status: which jails are active
sudo fail2ban-client status

# One jail: currently/total banned IPs
sudo fail2ban-client status sshd

# Ban / unban manually
sudo fail2ban-client set sshd banip 203.0.113.10
sudo fail2ban-client set sshd unbanip 203.0.113.10

# Test a filter against a real log before trusting it
sudo fail2ban-regex /var/log/auth.log /etc/fail2ban/filter.d/sshd.conf

# Reload config after edits / restart a jail
sudo fail2ban-client reload
sudo systemctl reload fail2ban
```

Configuration lives in `/etc/fail2ban/jail.d/*.local` (never edit `.conf` files directly): enable the jail, set `bantime`, `findtime`, `maxretry`, and `ignoreip` for your own management networks.

## logwatch
Parses system logs and emails/prints a human summary per service and time range.

```bash
# Yesterday's summary for one service, high detail
logwatch --service SSHD --range Yesterday --detail High

# Last hour, everything
logwatch --range "Today 10:00 - Today 11:00"

# Where does it send output? Check the config
grep -iE '^(MailTo|Range|Detail|Output)' /etc/logwatch/conf/logwatch.conf

# Debug what logwatch actually finds/parses
logwatch --detail Xhigh --range Today
```

By default it runs daily from cron and mails root; set `Output = file` + `Detail = High` if you want the report kept on disk instead.

## auditd
The Linux kernel audit system: permanent, tamper-evident rules about file access, syscalls and privilege use.

```bash
# Watch a file for writes/attribute changes, tagged "passwd_watch"
sudo auditctl -w /etc/passwd -p wa -k passwd_watch

# Search the audit log by that key
sudo ausearch -k passwd_watch --start today

# List loaded rules / remove them all (rules added with auditctl are volatile!)
sudo auditctl -l
sudo auditctl -D

# Reports: summary of executed commands, logins, events
sudo aureport --summary
sudo aureport -au          # authentication events
sudo aureport -x           # executed programs

# Load persistent rules and lock them until reboot
sudo augenrules --load
sudo augenrules --load --locked
```

Persistent rules go in `/etc/audit/rules.d/*.rules` (processed by `augenrules` into `/etc/audit/audit.rules`); `auditctl` one-liners disappear on reboot, so always finish testing by moving them into a rules file.