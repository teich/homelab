# Media LXC Container

Steps to create my media LXC docker container (turtles all the way down)

1. Follow the [lxc](lxc.md) to get a generic LXC container 
2. Follow the [Docker + LXC](docker-lxc.md) instructions
3. NFS mount media
4. 

## NFS Mount Media

Go into the GUI and NFS mount.
then edit the file and add 
mp0: /mnt/pve/media,mp=/mnt/media

<!-- ```
sudo apt install nfs-common
sudo mkdir -p /mnt/media
sudo mount -t nfs 192.168.1.10:/volume1/Media /mnt/media
sudo echo "192.168.1.10:/volume1/Media /mnt/media  nfs      defaults    0       0" >> /etc/fstab
``` -->

<!-- lxc.mount.entry=192.168.1.10:/volume1/Media /mnt/media nfs rw 0 0 -->
