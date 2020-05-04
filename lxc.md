## Enabling Docker in LXC

In `/etc/pve/local/lxc/<ID>.conf` append

```
features: keyctl=1,nesting=1
```

Found instructions in [this forum post](https://discuss.linuxcontainers.org/t/working-install-of-docker-ce-in-lxc-unprivileged-container-in-proxmox/3828)

## Generic Creating LXC tips
* Console never responded
* Ran `pct enter <ID>` to get into the LXC, then 

```
apt update && apt upgrade
apt install openssh-server
systemctl start sshd
systemctl status ssh
```