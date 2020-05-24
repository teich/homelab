I wanted passthrough GPU support, and it seemed easier to setup a dedicated Plex Media Server LXC container than mess around with VMs or nested Docker

Created a **Privileged container**

```
root@nuc:/etc/pve/lxc# cat 201.conf
arch: amd64
cores: 2
hostname: pms
memory: 2048
net0: name=eth0,bridge=vmbr0,firewall=1,hwaddr=9A:30:8C:86:1C:D2,ip=dhcp,type=veth
onboot: 1
ostype: debian
rootfs: local-zfs:subvol-201-disk-0,size=50G
swap: 512
lxc.cgroup.devices.allow: c 226:0 rwm
lxc.cgroup.devices.allow: c 226:128 rwm
lxc.cgroup.devices.allow: c 29:0 rwm
lxc.autodev: 1
lxc.hook.autodev: /var/lib/lxc/201/mount_hook.sh
lxc.apparmor.profile: unconfined
```

The `*.devices.allow` line above is the passthrough for the GPU.
The `lxc.apparmor.profile: unconfied` is to allow NFS to work in the container. Yes, I could have mounted it and passed it through, but I'm trying this for now.

`/var/lib/lxc/201/mount_hook.sh` contains:

```
mkdir -p ${LXC_ROOTFS_MOUNT}/dev/dri
mknod -m 666 ${LXC_ROOTFS_MOUNT}/dev/dri/card0 c 226 0
mknod -m 666 ${LXC_ROOTFS_MOUNT}/dev/dri/renderD128 c 226 128
mknod -m 666 ${LXC_ROOTFS_MOUNT}/dev/fb0 c 29 0
```

Then to install PMS, in the container:

```
apt update
apt upgrade
apt install curl gnupg2 nfs-common sudo
wget https://downloads.plex.tv/plex-media-server-new/1.19.3.2764-ef515a800/debian/plexmediaserver_1.19.3.2764-ef515a800_amd64.deb
dpkg -i plexmediaserver_1.19.3.2764-ef515a800_amd64.deb 

mkdir /mnt/media
mount 192.168.1.10:/volume1/Media /mnt/media

echo deb https://downloads.plex.tv/repo/deb public main | sudo tee /etc/apt/sources.list.d/plexmediaserver.list
curl https://downloads.plex.tv/plex-keys/PlexSign.key | sudo apt-key add -
apt update
```