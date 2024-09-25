---
title: nvme-cli
tags:
  - linux
---

https://github.com/linux-nvme/nvme-cli is a NVMe management command line interface.

## Install

```sh
sudo apt install nvme-cli
```

## See information (including drive health)

```sh
# X is the drive number
sudo nvme smart-log /dev/nvmeX -H
```
