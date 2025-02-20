---
title: Ubuntu 24.04 NTFS mount error
date: 2024-09-03
tags:
  - linux
---

```sh
echo 'blacklist ntfs3' | sudo tee /etc/modprobe.d/disable-ntfs3.conf
```
<!-- more -->

Ubuntu 24.04 (with kernel 6.8) may give an error while mounting NTFS partitions.

[Solution](https://bugs.launchpad.net/ubuntu/+source/ntfs-3g/+bug/2062972): disable the open source `ntfs3` driver and force Ubuntu to use the old `ntfs-3g` driver. Reboot to apply.

If the partition NTFS cannot be mounted, run `ntfsfix` to fix the problem.

```sh
sudo ntfsfix /dev/ntfsdevice
```
