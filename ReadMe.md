# Docker PiHole
PiHole hosted in docker.

## Port 53 In Use Fix

Disable port 53 from system resolve.

What to do:
1. `systemctl disable systemd-resolved.service`
2. `systemctl stop systemd-resolved`
3. `sudo nano edit /etc/systemd/resolved.conf`
4. Note: edit the file below (DNSStubListener=no) its there just change yes to no.
5. `service systemd-resolved restart`

Broke internet after port 53 changes.

Only check the file below don't edit it.

`sudo nano /etc/resolv.conf`


>When the Port 53 is already in Use, you can check this with this command (ubuntu):
Port 53 is being used at your host machine, that's why you can not bind 53 to host.
To find what is using port 53 you can do: sudo lsof -i -P -n | grep LISTEN
I'm a 99.9% sure that systemd-resolved is what is listening to port 53.
To solve that you need to edit the /etc/systemd/resolved.conf and uncomment DNSStubListener and change it to no, so it looks like this: DNSStubListener=no
After that reboot your system or restart the service with service systemd-resolved restart