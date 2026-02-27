---
title: system monitor
tags:
  - linux
  - command-line
  - system-monitor
---

<!--more-->

## btop

[btop](https://github.com/aristocratos/btop) is a resource monitor written in C++ that shows usage and stats for processor, memory, disks, network and processes.

### Install

#### APT

```sh
sudo apt install btop
```

#### snap

```sh
sudo snap install btop
sudo snap connect btop:removable-media
```

Official binaries can be downloaded [here](https://github.com/aristocratos/btop/releases).

## Glances

[glances](https://github.com/nicolargo/glances) is a cross-platform advance system monitor for usage monitoring for CPU, RAM, Network, GPU, etc.

### Install

#### Install script

```sh
curl -L https://bit.ly/glances | bash
```

Or

```sh
wget -O- https://bit.ly/glances | bash
```

#### snap

```sh
sudo snap install glances
```

## nvtop

[nvtop](https://github.com/Syllo/nvtop) is a GPU process monitor for AMD, Intel and NVIDIA GPUs. The command is `nvtop`.

### Install

#### APT

```sh
sudo apt install nvtop
```

#### snap

```sh
sudo snap install nvtop
# Add the capability to kill processes inside nvtop
sudo snap connect nvtop:process-control
# Add the capability to inspect GPU information (fan, PCIe, power, etc)
sudo snap connect nvtop:hardware-observe
# AMDGPU process list support (read /proc/<pid>)
sudo snap connect nvtop:system-observe
# Temporary workaround to get per-process GPU usage (read /proc/<pid>/fdinfo)
sudo snap connect nvtop:kubernetes-support
```

## Bottom

[bottom](https://github.com/clementtsang/bottom) is a resource monitor written in Rust. The command is `btm`.

### Install

#### DEB

Download and install the [deb release](https://github.com/ClementTsang/bottom/releases/latest).

#### snap

```sh
sudo snap install bottom

# To allow the program to run as intended
sudo snap connect bottom:mount-observe
sudo snap connect bottom:hardware-observe
sudo snap connect bottom:system-observe
sudo snap connect bottom:process-control
```

## Mission center

[Mission center](https://gitlab.com/mission-center-devs/mission-center) is a Windows-like monitoring tool for your CPU, Memory, Disk, Network and GPU usage.

### Install

- [AppImage (x86_64)](https://gitlab.com/mission-center-devs/mission-center/-/jobs/10144675634/artifacts/raw/MissionCenter_v1.0.2-x86_64.AppImage)
- [Flatpak](https://flathub.org/apps/io.missioncenter.MissionCenter)
- [snap](https://snapcraft.io/mission-center)

## NeoHtop

[neohtop](https://github.com/Abdenasser/neohtop) is a MacOS-like monitoring tool for your system.

### Install

- [Download from the project page](https://abdenasser.github.io/neohtop/)

## Disk info

### udisks

[udisks](https://wiki.archlinux.org/title/Udisks) provides a daemon udisksd, that implements D-Bus interfaces used to query and manipulate storage devices, and a command-line tool [udisksctl](https://manpages.ubuntu.com/manpages/noble/man1/udisksctl.1.html), used to query and use the daemon.

To see your drive model:

```bash
udisksctl status
```

### nvme-cli

[nvme-cli](https://github.com/linux-nvme/nvme-cli)is a NVMe management command line interface.

Install

```sh
sudo apt install nvme-cli
```

See drive health

```sh
# X is the drive number
sudo nvme smart-log /dev/nvmeX -H
```
