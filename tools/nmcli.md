# Network Manager CLI

Configure, manage, and troubleshoot network connections on systems using NetworkManager.

## Usage
```bash
device (dev)      manage network interfaces
connection (con)  manage profiles (persistent configurations)
networking        networking state (on/off, connectivity)
monitor           follow changes in real time
general           NM status, logging, version
```

## Commands
```bash
# Status
nmcli general status
nmcli device status
nmcli connection show --active

# Details of an interface (addresses, gateway, DNS, DHCP lease)
nmcli device show <interface>

# Bring an interface up/down, or apply the profile
nmcli device connect <interface>
nmcli device disconnect <interface>
nmcli connection up <profile>

# WiFi
nmcli device wifi list
nmcli device wifi connect <SSID> password <key>

# Static IP on a profile
nmcli connection modify <profile> ipv4.method manual \
    ipv4.addresses 192.168.1.10/24 ipv4.gateway 192.168.1.1 \
    ipv4.dns "1.1.1.1 8.8.8.8"
nmcli connection up <profile>

# Add/remove a route without editing the whole profile
nmcli connection modify <profile> +ipv4.routes "10.0.0.0/8 192.168.1.1"
nmcli connection modify <profile> -ipv4.routes "10.0.0.0/8 192.168.1.1"

# Clone / delete a profile
nmcli connection clone <profile> <new-name>
nmcli connection delete <profile>

# Dump every property of a profile
nmcli -f ALL connection show <profile>

# Machine-readable output (jq-friendly)
nmcli -t -f DEVICE,TYPE,STATE device
nmcli -j connection show <profile>
```

## Notes

`nmcli` changes are persistent (profile-based). For a quick temporary test that must not touch the saved profile, use `nmcli device modify <interface> ...` and revert with `nmcli connection up <profile>` (or `nmcli dev set <interface> managed no` to hand the interface over to another tool).

## References
- https://nmcli.com/
- https://networkmanager.dev/docs/api/latest/nmcli.html
