---
title: HAProxy to Home Network Nextcloud Server
layout: post
category: servers
tags: nextcloud vpn proxy raspberrypi letsencrypt tinc haproxy aws cloudflare
---

I managed to get a reverse proxy setup to serve to my in-progress home nextcloud server.
Using this [tinc vpn tutorial](https://jordancrawford.kiwi/setting-up-tinc/)
and adapting this [HAProxy Configuration](https://github.com/nextcloud/nextcloud-snap/wiki/Putting-the-snap-behind-a-reverse-proxy)
I managed to get everything working as expected, eventually.

## Gotchas

# Tinc

Tinc needs every host file to have the subnet information or the network
routes will not be setup correctly. Also be sure to open port 655 in
firewalls, both tcp and udp.

# HAProxy

This was fairly straightforward. Just stick everything at the bottom of
/etc/haproxy/haproxy.cfg, changing the localhost ip to the vpn ip of the
server.

`tail -f /var/log/haproxy.log` was very useful.

Even when using ports 80 and 443, the explicit port numbers seem to be
required in the backend config.

Some port forwarding stuff seems to be weirdly persistent, though that seems
to have been my cache.

# Let's Encrypt

I ended up leaving the snap listening on ports 80 and 443 because so that the
let's encrypt certs would just work. Let's Encrypt does not like port
forwarding.

# Cloudflare

Adding cloudflare's proxy to my own seems to work and not have any bad
performance implications. Note error 522 is a cloudflare error where the server is
unreachable.
