---
title: Reload nvidia GPU driver
date: 2024-08-07
tags:
  - linux
  - gpu
---

How to reload nvidia GPU driver to fix "NVML: Driver/library version mismatch" error after installing new nvidia driver. No rebooting required. [^1]

<!--more-->

The following command will switch the system into text (CLI) mode, reload the graphical driver, and then switch back to GUI mode.

```bash
sudo apt purge $DRIVER_TO_DELETE
sudo apt reinstall $DRIVER_OF_CHOICE

sudo systemctl isolate multi-user.target

lsmod | grep nvidia # - to identify the modules needing to be reloaded.
sudo modprobe --remove $ALL_MODULES_IDENTIFIED_ABOVE
sudo modprobe $ALL_MODULES_IDENTIFIED_ABOVE

sudo systemctl isolate graphical.target
```

[^1]: https://forums.developer.nvidia.com/t/how-to-fix-nvml-driver-library-version-mismatch-without-rebooting/269998
