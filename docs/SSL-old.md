Log into Proxmox as root

### Get Certs with Acme.sh 

```
wget -O -  https://get.acme.sh | sh
```

Get a token from DNSimple's ACCOUNT page (not user!)
The acme script below will automatically setup cron to renew the cert.

```
export DNSimple_OAUTH_TOKEN=YOURTOKENHERE
~/.acme.sh/acme.sh --issue --dns dns_dnsimple -d nuc.t.teich.network
```

### Setup Proxmox SSL:

```
/root/.acme.sh/acme.sh  --installcert  -d nuc.t.teich.network  \
    --certpath /etc/pve/local/pveproxy-ssl.pem \
    --keypath /etc/pve/local/pveproxy-ssl.key  \
    --capath  /etc/pve/local/pveproxy-ssl.pem  \
    --reloadcmd  "systemctl restart pveproxy"
```

SSH into my proxy host

```
sudo su - 
mkdir /mnt/SSL
mount toodle.local:/volume1/SSL /mnt/SSL
echo "toodle.local:/volume1/SSL /mnt/SSL  nfs      defaults    0       0" | tee -a /etc/fstab
cd ~/
curl https://get.acme.sh | sh
export DNSimple_OAUTH_TOKEN='TOKEN'
~/.acme.sh/acme.sh --issue --dns dns_dnsimple -d *.t.teich.network
mkdir -p /mnt/SSL/certs/*.t.teich.network
~/.acme.sh/acme.sh  --force --installcert  -d *.t.teich.network  \
    --cert-file /mnt/SSL/certs/*.t.teich.network/cert.pem \
    --key-file /mnt/SSL/certs/*.t.teich.network/certskey.pem  \
    --fullchain-file  /mnt/SSL/certs/*.t.teich.network/fullchain.pem  
```


## Proxies to explore
vouch
https://www.pomerium.io/