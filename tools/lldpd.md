# lldpd

lldpd is the daemon for the Link Layer Discovery Protocol (LLDP), a discovery protocol.
Why do I consider it a tool?
When managing networks, you cannot always rely on documentation, especially if you did not prepare it yourself. This tool provides us with information such as the device we are connected to at the other end of the cable, its management IP, whether there is VLAN tagging, the remote port, etc. It is particularly useful in network audits.

## Usage
```bash
lldpd       the daemon: sends and receives LLDP frames
lldpctl     the CLI: shows what the daemon learned about neighbors
lldpcli     the CLI used to configure the daemon (lldpctl is a compat alias)

Daemon options:
-d        do not daemonize; repeat for more verbosity (debugging)
-r        receive-only mode (listen, never send)
-k        hide kernel release/version/machine from the description
-S        override the system (chassis) description
-P        override the CDP platform name
-x/-X     enable the SNMP AgentX subagent (optionally on a specific socket)
-m        which management addresses/IPs to advertise (wildcards allowed)
-I        which interfaces to listen/send on (wildcards, ! to exclude)
-c/-e/-f/-s  also speak CDP / EDP / FDP / SONMP for legacy peers
```

## Customization

`/etc/lldpd.conf` (and drop-ins in `/etc/lldpd.d/`) holds `lldpcli configure` commands, executed at daemon start. What we advertise is what lets a remote admin identify us back:

```
configure system hostname "core-01.lab.example.com"
configure system description "datacenter core switch"
configure system interface pattern "*,!lo,!tun*"
configure lldp tx-interval 30
configure ports eth0 lldp portdescription "uplink to dist-02"
```

## Commands
```bash
# All neighbors, human readable
sudo lldpctl

# One interface only / compact one-line-per-neighbor view
sudo lldpctl <interface>
sudo lldpcli show neighbors summary

# Machine-readable for scripts/automation
sudo lldpctl -f keyvalue
sudo lldpctl -f json | jq '.lldp.devices[] | {name: .chassis.name, if: .port.descr}'

# What are we advertising, and how?
sudo lldpcli show commands
sudo lldpcli show interfaces details

# Run the daemon in the foreground, very verbose, for troubleshooting
sudo lldpd -ddddd
```

## References

- https://410g0n3.medium.com/lldp-and-uncommon-functionalities-82459b599418
- https://github.com/lldpd/lldpd
- man lldpd(8), lldpctl(8), lldpcli(8)
