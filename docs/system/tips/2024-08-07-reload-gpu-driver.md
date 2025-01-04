---
title: Reload nvidia GPU driver
date: 2024-08-07
tags:
  - linux
  - gpu
  - driver
categories:
  - system
---

Reload nvidia GPU driver to fix "NVML: Driver/library version mismatch" error without rebooting. [Source](https://forums.developer.nvidia.com/t/how-to-fix-nvml-driver-library-version-mismatch-without-rebooting/269998)

<!-- more -->

```bash
sudo apt purge $DRIVER_TO_DELETE
sudo apt reinstall $DRIVER_OF_CHOICE

sudo systemctl isolate multi-user.target

lsmod | grep nvidia # - to identify the modules needing to be reloaded.
sudo moprobe --remove $ALL_MODULES_IDENTIFIED_ABOVE
sudo insmod $ALL_MODULES_IDENTIFIED_ABOVE

sudo systemctl isolate graphical.target
```
