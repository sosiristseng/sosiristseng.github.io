---
title: Mount NAS drive in Linux at boot
date: 2024-04-23
tags:
  - linux
---

Add the following entry to `/etc/fstab` to automatically mount NAS drives at boot

<!-- more -->

```txt title="/etc/fstab"
//NAS_IP/directory /mnt/point cifs credentials=/home/user/.nascred,uid=1000,gid=1000,x-systemd.automount,x-systemd.mount-timeout=10  0  0
```

```txt title="/home/user/.nascred"
username=your_username
password=your_password
```
