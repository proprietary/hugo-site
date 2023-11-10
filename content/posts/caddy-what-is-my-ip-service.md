+++
title = 'Run your own "What Is My Ip?" service with Caddy and Cloudflare'
date = 2023-11-10T00:37:40-08:00
draft = false
+++

[Caddy](https://caddyserver.com/) is a well-known HTTP server that does much of what `nginx` does but with much simpler configuration. Here is an example of using Caddy to serve your own "What is my IP?" server.

There are services like ["ipify.org"](https://www.ipify.org/) where you just `$ curl https://api.ipify.org` and it returns your IP address. There is also [`http://checkip.amazonaws.com`](http://checkip.amazonaws.com), among many others. However, you may not want to rely on the uptime of these free third-party sites, you may not want third-parties logging your programmatic IP address queries, or you may just not want to abuse their services. Whatever the reason, this is how you would host your own version of that in the most simple and painless manner.

First, on some EC2 instance or VPS, follow the appropriate instructions to [install and run Caddy](https://caddyserver.com/docs/install) and expose ports `80` and `443` as usual.

Second, I'm making an assumption that you, like most people these days, are using Cloudflare as a transparent proxy between your server and the public internet.

Run this command to add the relevant section to your `Caddyfile`, replacing `<your-domain-here>` with your own domain like `ip.zelcon.net` in my case.

```bash
cat <<EOF >> /etc/caddy/Caddyfile
<your-domain-here> {
        respond * 200 {
                body "{http.request.header.CF-Connecting-IP}"
                close
        }
}
EOF
```

Explanation: Cloudflare passes the true client's IP in a header named "CF-Connecting-IP". Were you to simply grab the remote address of the incoming socket, you would get one of Cloudflare's IP addresses.

And that's it! As an example, you can test mine (which is hopefully still running whenever you're reading this) by doing the following:

```bash
curl https://ip.zelcon.net
# ... your IPv4 address shows up here

curl -6 https://ip.zelcon.net
# ... your IPv6 address shows up here (or an error message if your network interface does not have IPv6)
```
