```
apt update
apt dist-upgrade
apt install sudo gnupg
```

Tailscale:
```
curl https://pkgs.tailscale.com/stable/debian/buster.gpg | sudo apt-key add -
curl https://pkgs.tailscale.com/stable/debian/buster.list | sudo tee /etc/apt/sources.list.d/tailscale.list
sudo apt-get update
sudo apt-get install tailscale
sudo tailscale up
```

Then [visit the console](https://login2.tailscale.io/admin/machines) and disable key expiry for the new machine
