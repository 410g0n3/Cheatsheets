# hping3

packet crafter / TCP/IP tester (like ping but for TCP/UDP/ICMP)

## Usage
```bash
-0/-1/-2    raw IP / ICMP / UDP mode (default is TCP)
-S          set SYN flag (-A ACK, -F FIN, -R RST, -U UDP, ...)
-c          count of packets to send
-i          interval between packets (e.g. u100 for 100 us)
-d          data size in bytes (payload)
-t          TTL
-s          source port          -p destination port
-g          baseport for scanning
-f          flood mode (as fast as possible, no replies shown)
--rand-source  spoof random source IPs (Do NOT use on production networks)
--traceroute   traceroute mode
-I        interface
-n        numeric output
-q        quiet (summary only)      -v verbose
```

## Commands
```bash
# Ping a destination with 4 ICMP ping requests:
hping3 --icmp --count 4 ip_or_hostname

# Ping an IP address on port 80:
hping3 --destport 80 --syn ip_or_hostname

# Scan TCP port 80, scanning from the specific local source port 5090:
hping3 --verbose --syn --destport 80 --baseport 5090 ip_or_hostname

# Traceroute using a TCP scan to a specific destination port:
hping3 --traceroute --verbose --syn --destport 80 ip_or_hostname

# Scan a set of TCP ports on a specific IP address:
hping3 --scan 80,3000,9000 --syn ip_or_hostname

# Perform a TCP ACK scan to check if a given host is alive:
hping3 --count 2 --verbose --destport 80 --ack ip_or_hostname

# Path MTU probe: send one 1472-byte UDP packet (1500 bytes on the wire)
hping3 -2 -u 53 -d 1472 -c 1 -t 64 ip_or_hostname

# Perform a charge test on port 80:
hping3 --flood --destport 80 --syn ip_or_hostname
```

## Notes

Flood and `--rand-source` options generate real DoS traffic: use them only against equipment you own or are explicitly authorized to test.

## References
- https://github.com/antirez/hping
- https://www.hping.org/manpage.html
