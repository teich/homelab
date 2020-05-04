# Generic LCX setup tips

**Make sure to leave IPV6 to static (blank) to prevent long inbound network hangs**

There are a few things that I want 100% of the time, and some of the lower steps depend on:

*In the LXC container*
```
apt update && apt upgrade
apt install openssh-server curl sudo gnupg
```

## Tailscale

Per [this post](https://linux-tips.com/t/setup-openvpn-server-in-proxmox-lxc-container/695), we need to
hck the poor LXC container to enable `/dev/net/tun` by appending to /etc/pve/local/lcx/<ID>.conf:

*In Proxmox host OS*
```
lxc.mount.entry: /dev/net/tun dev/net/tun none bind,create=file
```

Then restart your container with 
```
pct stop <ID>
pct start <ID>
```

*Back in LXC container*
Then install [tailscale](https://tailscale.com/kb/1041/install-debian-buster)

```
curl https://pkgs.tailscale.com/stable/debian/buster.gpg | sudo apt-key add -
curl https://pkgs.tailscale.com/stable/debian/buster.list | sudo tee /etc/apt/sources.list.d/tailscale.list
sudo apt-get update
sudo apt-get install tailscale
sudo tailscale up

```