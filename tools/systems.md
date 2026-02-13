# Systems tool

## btop
A resource monitor that shows information about the CPU, memory, disks, network and processes.

```bash
btop
```

## lsof
List open files and the corresponding processes.

```bash
# List open ports by process and PID with no-resolution
sudo lsof -i -P -n
```

## ncdu
Disk usage analyzer with an ncurses interface.

```bash
ncdu
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
## specific incoming interface
ufw allow in on enp0s2 proto tcp port 22 comment "Allow SSH"
## specific source ip
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

## logwatch

## auditd