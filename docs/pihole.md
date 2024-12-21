# Issues configuring pihole

Setup:
- Ubuntu 20.04 headless-server

Problem:
Pihole installation broke. Failed on a step to resolve DNS. Server could not connect to internet after pihole installation changes.
Temporary fix is to edit /etc/resolv.conf to point to public DNS server, but this file would get reset on reboot.

Fix:
Delete symlink file (`/etc/resolv.conf`) and link it to `/run/systemd/resolve/resolv.conf` rather than `/run/systemd/resolve/stub-resolv.conf`

Edit `/etc/systemd/resolved.conf`. uncomment DNSStubListener and set to `no`. 

```bash
# Then...
sudo systemctl restart systemd-resolved.service
# Editing the config files in /etc is how to modify the daemons.
# It should have modified the file in /run/systemd/resolve/...

# Now replace the symlink
sudo rm /etc/resolve.conf
sudo ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf
```

Notes:
the systemd stub listener should not be enabled. Its ok if systemd-resolved is enabled, but not the stub resolver part (I think it uses the port it needs?)

Links:
https://askubuntu.com/questions/1394034/port-conflict-in-pi-hole-docker-installation-with-systemd-resolve-process
http://web.archive.org/web/20220612212822/https://www.bklynit.net/ubuntu-20-04-lts-docker-pihole/

