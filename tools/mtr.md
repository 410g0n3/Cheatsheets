# mtr

Combined traceroute + continuous ping: shows per-hop loss and latency statistics while the test keeps running.

## Usage
```bash
-r      report mode (text output, non-interactive)
-c      number of pings per host (default is endless in interactive mode)
-i      interval between pings in seconds
-p      split-up summary: one line per hop
--csv   CSV output, easy to parse
--no-dns  do not resolve hostnames (faster, avoids DNS noise)
-4/-6   force IPv4 / IPv6
-T      use TCP SYN probes instead of ICMP (bypasses ICMP policing)
-P      destination port for TCP probes
-I      interface to send from
```

## Commands
```bash
# Interactive test
sudo mtr <host>

# Report with one line per hop
sudo mtr --report --split <host>

# 20-cycle CSV report, no DNS resolution (great for evidence collection)
sudo mtr -r -c 20 --no-dns --csv <host> > mtr_$(date +%F).csv

# TCP mode to port 443 when intermediate routers deprioritize ICMP
sudo mtr -T -P 443 --report <host>
```

## Notes

Asterisks and high loss on early hops are usually ICMP TTL-exceeded messages being rate-limited (control-plane policing), not real forwarding loss: the way to tell them apart is to check whether the loss disappears at the last hop, and to confirm with `-T` mode.

## References
- https://github.com/traviscross/mtr
