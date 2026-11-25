# arp-scan
Send ARP packets to hosts (specified as IP addresses or hostnames) to scan the local network

## Usage

```bash
-I      select interface
-l      localnet
-v      verbose
-x      supress header and footer text
-Q      VLAN ID
-W      save pcap file
```

## Commands
```bash
sudo arp-scan -xlI <interface>
```

## References
https://github.com/royhills/arp-scan