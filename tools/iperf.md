# iPerf 3

Traffic generator for testing network bandwidth

## Usage
```bash
-s/-c     server / client mode
-p        port the server listens on (default 5201)
-P        number of parallel streams
-R        reverse direction (server sends to client)
-B        bidirectional test at the same time (iperf >= 3.16)
-t        duration of the test in seconds
-u        UDP mode (TCP is the default)
-b        target bitrate, essential for UDP (e.g. 1G, 100M)
-l        read/write buffer (payload) size
-w        socket buffer / window size
-O        omit N seconds at the start (skip TCP slow-start ramp for steady-state numbers)
-J        JSON output
```

## Commands
```bash
# Run iperf3 as a server:
iperf3 [-s|--server]

# Run an iperf3 server on a specific port:
iperf3 [-s|--server] [-p|--port] port

# Start bandwidth test:
iperf3 [-c|--client] server

# Run iperf3 in multiple parallel streams:
iperf3 [-c|--client] server [-P|--parallel] streams

# Reverse direction of the test. Server sends data to the client:
iperf3 [-c|--client] server [-R|--reverse]

# Both directions at the same time (saturate and check symmetric loss):
iperf3 -c server --bidir

# UDP test at a fixed rate: shows loss and jitter, not just throughput
iperf3 -c server -u -b 1G -t 30

# TCP with a larger window and 60 s duration, skipping the first 5 s
iperf3 -c server -t 60 -w 4M -O 5
```

## Notes

One iperf3 server process serves one test at a time: for parallel tests from several clients, run extra servers on different ports (`-p`). UDP `-b` defaults to a very low rate — always set it explicitly, and judge the result by loss/jitter, since UDP will show the configured rate even when the path can't carry it.

## References
- https://github.com/esnet/iperf
