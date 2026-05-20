---
title: nvme-cli
tags:
  - linux
  - command-line
  - system-monitor
  - disks
---

[nvme-cli](https://github.com/linux-nvme/nvme-cli)is a NVMe management command line interface.

## Install

```sh
sudo apt install nvme-cli
```

## Usage

See drive health

```sh
# X is the drive number
sudo nvme smart-log /dev/nvmeX -H
```
