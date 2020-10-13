# nginx-quic
with cloudflare quiche 
## Build 
- See this https://github.com/cloudflare/quiche/tree/master/extras/nginx
## http3 clients 
- use cloudflare sample
```
$ cargo build --examples
$ ./target/debug/examples/http3-client 
Usage: ./target/debug/examples/http3-client URL
```

## Check
```
$ netstat -an -p --udp | grep 443
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
udp        0      0 0.0.0.0:443             0.0.0.0:*   

$ RUST_LOG=info target/debug/examples/http3-client https://127.0.0.1
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```
## Server log
```
$ tail -f /opt/http3/nginx/logs/access.log 
127.0.0.1 - - [13/Oct/2020:07:43:12 +0000] "GET / HTTP/3" 200 612 "-" "quiche"
127.0.0.1 - - [13/Oct/2020:07:43:25 +0000] "GET / HTTP/3" 200 612 "-" "quiche"
```
