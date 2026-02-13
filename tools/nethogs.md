# nethogs

Monitor bandwidth usage per process.

## Usage
```bash
-d : delay for update refresh rate in seconds. default is 1.
-v : view mode (0 = KB/s, 1 = total KB, 2 = total B, 3 = total MB). default is 0.
-c : number of updates. default is 0 (unlimited).
-t : tracemode.
-p : sniff in promiscious mode (not recommended).
-s : sort output by sent column.
-a : monitor all devices, even loopback/stopped ones.
```

## Commands
```bash
# Show bandwith usage per process of one interface
sudo nethogs <interface>

# Show bandwidth usage in MB
sudo nethogs <interface> -v 3
```