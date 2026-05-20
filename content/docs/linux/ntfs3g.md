---
title: ntfs-3g
date: 2024-09-03
tags:
  - linux
  - windows
  - disk
---

## Replace `ntfs3` with `ntfs-3g`

Ubuntu 24.04 (with kernel 6.8) may give an error while mounting NTFS partitions. You can replace the default `ntfs3` driver with the good old `ntfs-3g` driver when the `ntfs3` driver does not work.

```sh
echo 'blacklist ntfs3' | sudo tee /etc/modprobe.d/disable-ntfs3.conf
sudo rmmod ntfs3
sudo apt install ntfs-3g
```

[Solution](https://bugs.launchpad.net/ubuntu/+source/ntfs-3g/+bug/2062972): disable the open source `ntfs3` driver and use the good old `ntfs-3g` driver.

If one NTFS partition cannot be mounted, run `ntfsfix` to fix it.

```sh
sudo ntfsfix /dev/ntfsdevice
```
