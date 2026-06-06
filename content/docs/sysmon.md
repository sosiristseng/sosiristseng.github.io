---
title: System monitor
tags:
  - windows
  - command-line
  - system-monitor
  - gpu
  - linux
---

Tools for monitoring system status (CPU, RAM, GPU, disks, network).

## General system monitors

### bottom

[bottom](https://github.com/ClementTsang/bottom) is a cross-platform graphical process/system monitor written in Rust.

**Install**

See the [instructions](https://github.com/ClementTsang/bottom#installation) in the README.

**Usage**

```sh
btm
```

### btop

[btop](https://github.com/aristocratos/btop) is a resource monitor written in C++ that shows usage and stats for processor, memory, disks, network and processes.

**Install**

```sh
sudo apt install btop
```

or

```sh
sudo snap install btop
sudo snap connect btop:removable-media
```

**Run**

```sh
btop
```

### Glances

[glances](https://github.com/nicolargo/glances) is a cross-platform advance system monitor for usage monitoring for CPU, RAM, Network, GPU, etc.

**Install and run**

```sh
## Update every 1 second
uvx glances -T1
```

### PSTOP

[pstop](https://github.com/psmux/pstop) is a HTOP-like TUI system monitor for Windows.

**Install**

```powershell
winget install marlocarlo.pstop
```

or

```powershell
choco install pstop
```

**Usage**

```powershell
pstop
```

or

```powershell
htop
```

### NeoHtop

[neohtop](https://github.com/Abdenasser/neohtop) is a MacOS-like monitoring tool for your system.

[Download from the project page](https://abdenasser.github.io/neohtop/).

### Mission center

[Mission center](https://gitlab.com/mission-center-devs/mission-center) is a Windows task manager-like monitoring tool for your CPU, Memory, Disk, Network and GPU usage.

**Install**

- [AppImage (x86_64)](https://gitlab.com/mission-center-devs/mission-center/-/jobs/10144675634/artifacts/raw/MissionCenter_v1.0.2-x86_64.AppImage)
- [Flatpak](https://flathub.org/apps/io.missioncenter.MissionCenter)
- [snap](https://snapcraft.io/mission-center)

## Monitoring GPU

### nvtop

[nvtop](https://github.com/Syllo/nvtop) is a GPU process monitor for AMD, Intel and NVIDIA GPUs.

**Install**

```sh
sudo apt install nvtop
```

or

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

**Usage**

```sh
nvtop
```

### nvitop

[nvitop](https://github.com/XuehaiPan/nvitop) is an interactive NVIDIA-GPU process viewer.

**Install**

```sh
uvx nvitop
```



## Monitoring Disks

### nvme-cli

[nvme-cli](https://github.com/linux-nvme/nvme-cli) is a NVMe management command line interface.

**Install**

```sh
sudo apt install nvme-cli
```

To see the drive health:

```sh
# X is the drive number
sudo nvme smart-log /dev/nvmeX -H
```

### udisks

[udisks](https://wiki.archlinux.org/title/Udisks) provides a daemon `udisksd`, that implements D-Bus interfaces used to query and manipulate storage devices, and a command-line tool [udisksctl](https://manpages.ubuntu.com/manpages/noble/man1/udisksctl.1.html), used to query and use the daemon.

To see the drive model:

```bash
udisksctl status
```
