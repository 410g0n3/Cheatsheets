# tcpdump

Packet capture / filter

## Usage
```bash
-i <interface>
-n <no resolve hostnames>
-nn <no resolve service names>
-v <verbose>
```

## Commands
- EtherType filter

```bash
# LACP
tcpdump -ni any ether proto 0x8809 -v

# LLDP
tcpdump -ni any ether proto 0x88cc -v

# ARP
tcpdump -ni any ether proto 0x0806 -v

# VLAN
tcpdump -ni any ether proto 0x8100 -v
```

- Basic filtering

```bash
# Capture 100 packets on interface eth0
sudo tcpdump -i <interface> -c 100 -nn -s 0

# Save http traffic to file
sudo tcpdump -i <interface> -s 0 -w http.pcap tcp port 80
```

## References
- Syntax generator:
    https://tcpdump101.com/