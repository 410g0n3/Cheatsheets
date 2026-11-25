# tcptraceroute

traceroute using TCP SYN packets. Able to bypass the most common firewall filters, since SYN probes to open/filtered ports look like normal connection attempts (equivalent to `traceroute -T`).

## Usage
```bash
-m      max TTL / maximum number of hops (default 30)
-q      number of probes per hop (default 3)
-i      interface to send from
-n      numeric output (no DNS resolution)
-f      first TTL to start probing from
host [port]   destination port defaults to 80
```

## Commands
```bash
# Trace to a host on port 80
tcptraceroute <host>

# Trace on a port you actually care about (443, 179, ...)
tcptraceroute <host> 443

# Limit hops and probes, no DNS
tcptraceroute -m 15 -q 1 -n <host> 53

# Modern alternative (iputils traceroute)
traceroute -T -p 443 <host>
```

## Notes

Interpretation differs from UDP traceroute: a SYN/ACK from an address means the destination is reachable (the port is open); a RST also means you reached the destination, just on a closed port. Silence until the end usually means a stateful device is dropping, not blackholing.

## References
- https://man.freebsd.org/cgi/man.cgi?query=tcptraceroute
