# dnstop
displays DNS querys in real time

## Usage
```bash
While dnstop is running, use these keys to toggle different display modes:
Key	Action / Display Mode
1	Show TLDs (Top-Level Domains like .com, .net, .org).
2	Show SLDs (Second-Level Domains google.com).
3	Show Third-Level Domains (api.google.com).
4	Show Fourth-Level Domains.
5   Show Five-Level Domains
6   Show Six-Level Domains
7   Show Seven-Level Domains
t	Show Query Types (A, AAAA, PTR, MX, NS, etc.).
r	Show Response Codes (NoError, NxDomain, ServFail).
s	Show Source IP Addresses (Who is making the requests).
d	Show Destination IP Addresses (Which DNS servers are being queried).
o	Show OpCodes (Standard query, Inverse query, Status).
```

## Commands
```bash
# show 7th level query names; press enter and then press 7 to see the querys
# also can press '&' to see the querys and sources
sudo dnstop -l 7 <interface>
```