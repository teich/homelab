# Media VM

Frist creat a VM (I did Debian 10)
Open a console and:

```
useradd -m <USERNAME>
passwd <USERNAME>
usermod -a -G sudo <USERNAME>
apt update
apt install openssh-server curl sudo gnupg qemu-guest-agent
```

Now logout and SSH in as the new user. 

## Install Tailscale

Source [instructions](https://tailscale.com/kb/1041/install-debian-buster)

```
sudo apt install gnupg
curl https://pkgs.tailscale.com/stable/debian/buster.gpg | sudo apt-key add -
curl https://pkgs.tailscale.com/stable/debian/buster.list | sudo tee /etc/apt/sources.list.d/tailscale.list
sudo apt-get update
sudo apt-get install tailscale
sudo tailscale up
```

Then [visit the console](https://login2.tailscale.io/admin/machines) and disable key expiry for the new machine

## Installing Docker

From [these instructions](https://docs.docker.com/engine/install/debian/)

```
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world
```

## NFS Mount Media

```
sudo apt install nfs-common
sudo mkdir -p /mnt/media
sudo mount -t nfs <NFS_SERVER>:/volume1/Media /mnt/media
echo "<NFS_SERVER>:/volume1/Media /mnt/media  nfs      defaults    0       0" | sudo tee -a /etc/fstab
```

## Setup Docker

```
mkdir -p /srv/docker
```
