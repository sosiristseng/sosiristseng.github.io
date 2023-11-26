---
title: General Linux Setup
tags:
  - linux
---

+ [[swap-setup|Setup swap]]
+ [[ubuntu-postinstall|Ubuntu post-install]]

## Install fonts

Copy the fonts files to `~/.local/share/fonts/`. Then, run `fc-cache` to rebuild the cache.

```sh
fc-cache -fv
```

## Let Linux use local time

When dual-booting Linux and Windows, one might want to set the clock to the local time zone in Linux[^localtime]

```bash
timedatectl set-local-rtc 1
```

[^localtime]: https://itsfoss.com/wrong-time-dual-boot/

## NAS setup

Add the following entry to `/etc/fstab` to automatically mount NAS drives at boot

```txt title="/etc/fstab"
//NAS_IP/directory /mnt/point  cifs  credentials=/etc/samba/credentials,uid=1000,gid=1000,_netdev,x-systemd.automount,x-systemd.mount-timeout=10  0  0
```
