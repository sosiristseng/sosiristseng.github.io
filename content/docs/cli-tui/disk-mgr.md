---
title: Disk management
tags:
  - command-line
  - linux
---

> Disk management in Linux

## udisks

[udisks](https://wiki.archlinux.org/title/Udisks) provides a daemon `udisksd`, that implements D-Bus interfaces used to query and manipulate storage devices, and a command-line tool [udisksctl](https://manpages.ubuntu.com/manpages/noble/man1/udisksctl.1.html), used to query and use the daemon.

To see the drive model:

```sh
udisksctl status
```

## nvme-cli

[nvme-cli](https://github.com/linux-nvme/nvme-cli) is a NVMe management command line interface.

**Install**

```sh
sudo apt install nvme-cli
```

**Usage**

To see the drive health:

```sh
# change 0 to the drive number
sudo nvme smart-log /dev/nvme0 -H
```
