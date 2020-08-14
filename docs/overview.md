### media.t.teich.network
Lab: **SF**
Type: **VM**
Tailscale: **Yes**
Needs SSL: **Yes**
Docker root directory: `/srv/docker` 
Docker compose: `/srv/docker/homelab/docker-compose.yml`

### mineos.t.teich.network
Lab: **SF**
Type: **LXC**
Tailscale: **Yes**
Needs SSL: **Yes**

Update mineos-node:
```
cd /usr/games/minecraft
git pull
```

### pms (no DNS)
Lab: **SF**
Type: **LXC**
Tailscale: **No**
Needs SSL: **No**
Notes: plex installed via apt, update with normal `apt update`

### ha.t.teich.network
Lab: **SF**
Type: **VM**
Tailscale: **Yes**
Needs SSL: **Yes**

### unifi.t.teich.network	
Lab: **BV**
Type: **LXC**
Tailscale: **Yes**
Needs SSL: **No**
OS: Ubuntu 20
Login: root/SSH key
Notes: Unifi installed via apt, update with normal `apt update`

### mineos-bv.b.teich.network
Lab: **BV**
Type: **LXC**
Tailscale: **No**
Needs SSL: **Maybe?**
OS: Ubuntu 20

Mineos Update:
```
cd /usr/games/minecraft
git pull
```

### unms.t.teich.network
Lab: **BV**
Type: **VM**
Tailscale: **Yes**
Needs SSL: **Maybe?**
OS: Ubuntu 20
Updates: Via UNMS web UI

### tick.t.teich.network
Lab: **BV**
Type: **VM**
Tailscale: **Yes**
Needs SSL: **Maybe?**
OS: Ubuntu 20
`/home/oren/docker-compose.yaml` because ¯\_(ツ)_/¯

