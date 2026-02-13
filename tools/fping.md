# fping

Ping many hosts quickly

## Usage
```bash
-I      interface
-a      show targets that are alive
-g      generate target list
-S      set source IP
```

## Commands
```bash
# Ping IP range and print only alive hosts
fping -a -g 192.168.0.100 192.168.0.150 2>/dev/null

# Ping entire CIDR and print only alive hosts
fping -a -g 192.168.0.0/24 -I eth0 2>/dev/null

# Ping from file
fping -a < hosts.txt 2>/dev/null

```