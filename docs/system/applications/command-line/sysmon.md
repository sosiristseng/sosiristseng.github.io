---
title: System monitor
tags:
  - linux
  - command-line
---

## btop

https://github.com/aristocratos/btop is a resource monitor written in C++ that shows usage and stats for processor, memory, disks, network and processes.

### Install

=== "Arch Linux"

```sh
sudo pacman -S btop
```

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

=== "Arch Linux"

    ```sh
    sudo pacman -S glances
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

=== "Arch Linux"

    ```sh
    sudo pacman -S nvtop
    ```

## Bottom

https://github.com/clementtsang/bottom is a resource monitor written in Rust. The command is `btm`.

### Install

=== "Ubuntu"

    Download and install the [deb release](https://github.com/ClementTsang/bottom/releases/latest).

=== "Arch Linux"

    ```sh
    sudo pacman -S bottom
    ```

=== "snap"

    ```sh
    sudo snap install bottom

    # To allow the program to run as intended
    sudo snap connect bottom:mount-observe
    sudo snap connect bottom:hardware-observe
    sudo snap connect bottom:system-observe
    sudo snap connect bottom:process-control
    ```

=== "Windows"

    Chocolatey:

    ```powershell
    choco install bottom
    ```

    winget:

    ```powershell
    winget install bottom
    ```
