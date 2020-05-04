Need to automate this. In the meantime, here are notes on homelab setup

In `/etc/pve/local/lxc/<ID>.conf` append

```
features: keyctl=1,nesting=1
```


## Setup MineOS
From [these instructions](https://github.com/hexparrot/mineos-node)

```
curl -sL https://deb.nodesource.com/setup_8.x | bash -
apt-get update
apt-get install -y nodejs git rdiff-backup screen build-essential openjdk-8-jre-headless
mkdir -p /usr/games
cd /usr/games
git clone https://github.com/hexparrot/mineos-node.git minecraft
cd minecraft
chmod +x generate-sslcert.sh
./generate-sslcert.sh
cp mineos.conf /etc/mineos.conf
npm install
```

Then enable it

```
cp /usr/games/minecraft/init/systemd_conf /etc/systemd/system/mineos.service
systemctl enable mineos
systemctl start mineos
```