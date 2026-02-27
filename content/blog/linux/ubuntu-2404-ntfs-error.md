---
title: Ubuntu 24.04 NTFS mount error
date: 2024-09-03
tags:
  - linux
---

Use the `ntfs3-3g` driver instead of the default `ntfs3` driver.

<!--more-->

```sh
echo 'blacklist ntfs3' | sudo tee /etc/modprobe.d/disable-ntfs3.conf
sudo rmmod ntfs3
sudo apt install ntfs-3g
```

Ubuntu 24.04 (with kernel 6.8) may give an error while mounting NTFS partitions.

[Solution](https://bugs.launchpad.net/ubuntu/+source/ntfs-3g/+bug/2062972): disable the open source `ntfs3` driver and use the good old `ntfs-3g` driver.

If one NTFS partition cannot be mounted, run `ntfsfix` to fix it.

```sh
sudo ntfsfix /dev/ntfsdevice
```
