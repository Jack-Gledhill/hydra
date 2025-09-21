## Why two Services?

One is for the DNS server, the other is for the web interface. 
The DNS Service is exposed via [MetalLB](https://metallb.io), the web interface is exposed via [Traefik](https://traefik.io).

I could put them both in one service, but then the web interface would technically be accessible via the Load Balancer IP, which is not ideal since it's not protected by SSL.
The actual risk here is minimal, but the fix is very simple so might as well take the win.