---
title: nvtop
tags:
  - linux
  - command-line
  - system-monitor
  - gpu
---

[nvtop](https://github.com/Syllo/nvtop) is a GPU process monitor for AMD, Intel and NVIDIA GPUs.

## Install

**apt**

```sh
sudo apt install nvtop
```

**snap**

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

## Run

```sh
nvtop
```
