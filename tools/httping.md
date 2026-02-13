# httping

measure HTTP/HTTPS reachability and latency.

## Commands

```bash
# Ping the specified URL
httping -g url

# Ping the web server on host and port
httping -h host -p port

# Ping the web server on host using a TLS connection
httping -l -g https://host

# Ping the web server on host using HTTP basic authentication
httping -g http://host -U username -P password
```

## Notes

It works by performing a HEAD request, so it is not silent and will leave a trace in the server logs.<br>To be more discreet, it is recommended to use hping3.