## Generic Creating LXC tips
* Console never responded
* Ran `pct enter <ID>` to get into the LXC, then 

```
apt update && apt upgrade
apt install openssh-server curl sudo
systemctl start sshd
systemctl status ssh
```

Hack the poor LXC container to enable `/dev/net/tun` by appending to /etc/pve/local/lcx/<ID>.conf:

```
lxc.cgroup.devices.allow = c 10:200 rwm
lxc.hook.autodev = sh -c "modprobe tun; cd ${LXC_ROOTFS_MOUNT}/dev; mkdir net; mknod net/tun c 10 200; chmod 0666 net/tun"
```
Then install [tailscale](https://tailscale.com/kb/1041/install-debian-buster)

```
curl https://pkgs.tailscale.com/stable/debian/buster.gpg | sudo apt-key add -
curl https://pkgs.tailscale.com/stable/debian/buster.list | sudo tee /etc/apt/sources.list.d/tailscale.list

sudo apt-get update
sudo apt-get install tailscale

```
## Enabling Docker in LXC

In `/etc/pve/local/lxc/<ID>.conf` append

```
features: keyctl=1,nesting=1
```

Found instructions in [this forum post](https://discuss.linuxcontainers.org/t/working-install-of-docker-ce-in-lxc-unprivileged-container-in-proxmox/3828)
