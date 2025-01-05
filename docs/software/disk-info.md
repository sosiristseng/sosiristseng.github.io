---
title: Disk info
tags:
  - linux
  - command-line
---

## udisks

[udisks](https://wiki.archlinux.org/title/Udisks) provides a daemon udisksd, that implements D-Bus interfaces used to query and manipulate storage devices, and a command-line tool [udisksctl](https://manpages.ubuntu.com/manpages/noble/man1/udisksctl.1.html), used to query and use the daemon.

### See drive model

```bash
udisksctl status
```

## nvme-cli

https://github.com/linux-nvme/nvme-cli is a NVMe management command line interface.

### Install

```sh
sudo apt install nvme-cli
```

### See drive health

```sh
# X is the drive number
sudo nvme smart-log /dev/nvmeX -H
```
