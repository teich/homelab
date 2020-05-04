# Instructions for getting Docker + Debian 10 + LXC container working

## Enabling Docker in LXC

After the LXC container is created:

*In Proxmox host OS*
In `/etc/pve/local/lxc/<ID>.conf` append

```
features: keyctl=1,nesting=1
```

then restart the container

Found instructions in [this forum post](https://discuss.linuxcontainers.org/t/working-install-of-docker-ce-in-lxc-unprivileged-container-in-proxmox/3828)

## Installing Docker

Following [these instructions](https://docs.docker.com/engine/install/debian/)

```
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

Then check it's all working with `sudo docker run hello-world`