---
title: CUDA
tags:
  - linux
  - gpu
---

Setup CUDA for NVIDIA GPUs.

<!--more-->

## Setup CUDA

### From the Ubuntu repository

> Recommended for Ubuntu 26.04 and later.

```sh
sudo ubuntu-drivers list
sudo ubuntu-drivers install  # Install the recommended driver
sudo apt install cuda-toolkit
```

### From nvidia

Install nvidia CUDA runtime and compatible GPU driver from NVIDIA: https://developer.nvidia.com/cuda-toolkit (*For Ubuntu 26.04*)

First clear previous nvidia drivers and CUDA installations.

```bash
sudo apt remove --purge '*cuda*' '*nvidia*'
```

Then install drivers

```sh
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2604/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update && sudo apt-get -y install cuda-toolkit-13-4
```

Add the CUDA compiler (`nvcc`) and its libraries to your `PATH`:

```sh {filename="~/.profile"}
export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```

See [docker](docker.md) for how to setup docker containers running CUDA.

## Tweaks

[ArchWiki: NVIDIA/Tips and tricks](https://wiki.archlinux.org/title/NVIDIA/Tips_and_tricks)

### Power limit

To monitor GPU power draw:

```bash
nvidia-smi -q -d POWER -l 1 | grep "Power Draw"
```

To limit power draw to 300W, this setting will be lost after reboot.

```bash
sudo nvidia-smi -pl 300
```

To apply your power draw setting at boot, make it a systemd service.

```txt {filename="/etc/systemd/system/nvidia-tdp.timer"}
[Unit]
Description=Set NVIDIA power limit on boot

[Timer]
OnBootSec=5

[Install]
WantedBy=timers.target
```

```txt {filename="title=/etc/systemd/system/nvidia-tdp.service"}
[Unit]
Description=Set NVIDIA power limit

[Service]
Type=oneshot
ExecStart=/usr/bin/nvidia-smi -pl 300
```

And enable `nvidia-tdp.timer`.

```sh
sudo systemctl enable nvidia-tdp.timer
```

### Lock GPU frequency

To lock the GPU frequency from 0 to 2200 MHz, run the following command

```sh
sudo nvidia-smi -lgc 0,2200
```

To make to change persistent over reboots, one can use the similar method above or use [Spark Limiter](https://github.com/MiaAI-Lab/sparkLimiter) to re-apply the setting at boot.

### Monitor GPU activities

- `nvidia-smi`
- `nvtop`
- `nvitop`

### Reload nvidia GPU driver

How to reload nvidia GPU driver to fix "NVML: Driver/library version mismatch" error after installing new nvidia driver. No rebooting required. [^1]

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
