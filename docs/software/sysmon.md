---
title: System monitor
tags:
  - linux
  - command-line
  - system-monitor
---

## btop

https://github.com/aristocratos/btop is a resource monitor written in C++ that shows usage and stats for processor, memory, disks, network and processes.

### Install

=== "Ubuntu"

```sh
sudo apt install btop
```

=== "snap"

```sh
sudo snap install btop
sudo snap connect btop:removable-media
```

=== "Binary executable"

Official binaries can be downloaded [here](https://github.com/aristocratos/btop/releases).

## Glances

https://github.com/nicolargo/glances is a cross-platform advance system monitor for usage monitoring for CPU, RAM, Network, GPU, etc.

### Install

=== "Install script"

    ```sh
    curl -L https://bit.ly/glances | bash
    ```

    Or

    ```sh
    wget -O- https://bit.ly/glances | bash
    ```

=== "Ubuntu"

    ```sh
    sudo apt update && sudo apt install python3-psutil

    pip install glances --upgrade --user
    # NVIDIA GPU support
    pip install glances[gpu] --upgrade --user
    ```

## nvtop

https://github.com/Syllo/nvtop is a GPU process monitor for AMD, Intel and NVIDIA GPUs.

### Install

=== "Ubuntu"

    ```sh
    sudo apt install nvtop
    ```

=== "snap"

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

https://github.com/clementtsang/bottom is a resource monitor written in Rust. The command is `btm`.

### Install

=== "Ubuntu"

    Download and install the [deb release](https://github.com/ClementTsang/bottom/releases/latest).

=== "snap"

    ```sh
    sudo snap install bottom

    # To allow the program to run as intended
    sudo snap connect bottom:mount-observe
    sudo snap connect bottom:hardware-observe
    sudo snap connect bottom:system-observe
    sudo snap connect bottom:process-control
    ```
