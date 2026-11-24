---
title: System monitor
tags:
  - command-line
  - system-monitor
  - gpu
  - linux
---

## Btop

[btop](https://github.com/aristocratos/btop) is a resource monitor written in C++ that shows usage and stats for processor, memory, disks, network and processes.

**Install**

Ubuntu:

```sh
sudo apt install btop
```

Snap:

```sh
sudo snap install btop
sudo snap connect btop:removable-media
```

Usage:

```sh
btop
```

## Bottom

[bottom](https://github.com/ClementTsang/bottom) is a cross-platform graphical process and system monitor written in Rust.

See the [instructions](https://github.com/ClementTsang/bottom#installation) in the README.

```sh
sudo snap install bottom

# To allow the program to run as intended
sudo snap connect bottom:mount-observe
sudo snap connect bottom:hardware-observe
sudo snap connect bottom:system-observe
sudo snap connect bottom:process-control
```

Usage

```sh
btm
```

## Glances

[glances](https://github.com/nicolargo/glances) is a cross-platform advance system monitor for usage monitoring for CPU, RAM, Network, GPU, etc.

**Install and run**

The simplest way to run glances is via the `uv` Python package manager.

```sh
## Update every 1 second
uvx glances -T1
```

## nvtop

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

## nvitop

[nvitop](https://github.com/XuehaiPan/nvitop) is an interactive NVIDIA-GPU process viewer.

**Install and run**

Using the `uv` Python package manager.

```sh
uvx nvitop
```
