# httping

measure HTTP/HTTPS reachability and latency.

## Usage
```bash
-g      URL to ping
-h/-p   host / port (when not using a full URL)
-c      count of requests (default: endless)
-i      interval between requests in seconds
-t      timeout in seconds per request
-l      use TLS (https)
-U/-P   username / password for HTTP basic authentication
-x      proxy to use (proxyhost:port)
-G      do a full GET instead of HEAD (measures transfer, not just latency)
-b      with -G: show throughput in KB/s
-o      expected HTTP status codes (e.g. -o 200,301)
-q      quiet
```

## Commands

```bash
# Ping the specified URL
httping -g url

# 20 requests, one per second
httping -c 20 -i 1 -g url

# Ping the web server on host and port
httping -h host -p port

# Ping the web server on host using a TLS connection
httping -l -g https://host

# Ping the web server on host using HTTP basic authentication
httping -g http://host -U username -P password

# Via a proxy
httping -x proxy_host:3128 -g http://url
```

## Notes

It works by performing a HEAD request, so it is not silent and will leave a trace in the server logs.<br>To be more discreet, it is recommended to use hping3.

## References
- https://www.vanheusden.com/httping/
