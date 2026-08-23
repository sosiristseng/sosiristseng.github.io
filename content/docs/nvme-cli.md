---
title: nvme-cli
tags:
  - command-line
  - linux
  - disk
---

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
