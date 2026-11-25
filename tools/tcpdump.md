# tcpdump

Packet capture / filter

## Usage
```bash
-i <interface>   capture on interface ("any" for all)
-n         no resolve hostnames
-nn        no resolve service names either
-v/-vv/-vvv  increasing verbosity
-c         stop after N packets
-s 0       capture full packets (default snaplen truncates)
-w         write pcap to file       -r read pcap from file
-e         show link-level (Ethernet/MAC) headers
-A/-X      ASCII / hex+ASCII payload display
-l         line-buffered (needed when piping to grep)
-Q in|out|inout   direction filter
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

# Host / subnet / port primitives
tcpdump -nn host 10.0.0.1
tcpdump -nn net 10.0.0.0/24 and not port 22
tcpdump -nn dst port 53 or src port 53

# Only connection attempts (SYN without ACK) toward a host
tcpdump -nn 'tcp[tcpflags] & (tcp-syn|tcp-ack) == tcp-syn' and dst host 10.0.0.1

# BGP sessions (keepalive/update flapping evidence)
tcpdump -nn 'tcp port 179 and (tcp[tcpflags] & tcp-rst != 0 or greater 68)'

# Specific VLAN
tcpdump -nn vlan 100 and host 10.0.0.1

# Multicast (e.g. OSPF hello)
tcpdump -nn 'ip proto 2 and host 224.0.0.5'
```

- Reading saved captures

```bash
# Replay a pcap
tcpdump -nnr capture.pcap

# Replay filtered: only one conversation
tcpdump -nnr capture.pcap host 10.0.0.1 and port 443
```

## Notes

`any` combined with `-e` is how you tell L2 loops and stale ARP apart from L3 problems; keep filters as BPF expressions in quotes so the shell does not eat `()`. Capture to `-w file.pcap` instead of console when you need to open the evidence later in Wireshark.

## References
- Syntax generator:
    https://tcpdump101.com/
- man tcpdump(8), pcap-filter(7)
