---
title: CUDA
date: 2025-02-20
tags:
- linux
- gpu
---

Setup CUDA for NVIDIA GPUs.

## Install drivers

### From the Ubuntu repository

```sh
sudo ubuntu-drivers install
```

### From nvidia

Install nvidia CUDA runtime and compatible GPU driver from NVIDIA: https://developer.nvidia.com/cuda-toolkit (*For Ubuntu 24.04*)

Clean previous installations

```bash
sudo apt autopurge 'cuda*' 'nvidia*'
```

Install drivers
```sh
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt update && sudo apt -y install cuda-toolkit-13-0
```

Add the CUDA compiler (`nvcc`) to the system `PATH`:

```sh title="~/.profile"
export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}
```

For WSL2, install Windows NVIDIA GPU driver first; then install the CUDA toolkit in the WSL.

```sh
wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-wsl-ubuntu.pinsudo mv cuda-wsl-ubuntu.pin /etc/apt/preferences.d/cuda-repository-pin-600wget https://developer.download.nvidia.com/compute/cuda/13.0.2/local_installers/cuda-repo-wsl-ubuntu-13-0-local_13.0.2-1_amd64.debsudo dpkg -i cuda-repo-wsl-ubuntu-13-0-local_13.0.2-1_amd64.debsudo cp /var/cuda-repo-wsl-ubuntu-13-0-local/cuda-*-keyring.gpg /usr/share/keyrings/sudo apt-get updatesudo apt-get -y install cuda-toolkit-13-0
```

## Tweaks

[ArchWiki: NVIDIA/Tips and tricks](https://wiki.archlinux.org/title/NVIDIA/Tips_and_tricks)

### Power limit

To monitor GPU power draw:
```bash
nvidia-smi -q -d POWER -l 1 | grep "Power Draw"
```

To limit power draw to 300W, the setting will reset after reboot.
```bash
sudo nvidia-smi -pl 300
```

To apply power draw settings at boot, make a systemd service.

```txt title="/etc/systemd/system/nvidia-tdp.timer"
[Unit]
Description=Set NVIDIA power limit on boot

[Timer]
OnBootSec=5

[Install]
WantedBy=timers.target
```

```txt title=/etc/systemd/system/nvidia-tdp.service""
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

### Preserve video memory after suspend

Fixes GUI corruptions after suspend and resume.

And the following file to preserve video memory after suspend.

```txt title="/etc/modprobe.d/nvidia.conf"
NVreg_PreserveVideoMemoryAllocations=1
NVreg_TemporaryFilePath=/var/tmp
```

## Monitor GPU activities

- `btop`
- `nvidia-smi`
- [[sysmon#nvtop]]
