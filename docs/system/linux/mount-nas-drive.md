---
title: Mount NAS drive in Linux
tags:
  - linux
---

Add the following entry to `/etc/fstab` to automatically mount NAS drives at boot

```txt title="/etc/fstab"
//NAS_IP/directory /mnt/point cifs credentials=/etc/samba/credentials,uid=1000,gid=1000,_netdev,x-systemd.automount,x-systemd.mount-timeout=10  0  0
```
