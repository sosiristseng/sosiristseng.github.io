---
title: glances
tags:
  - linux
  - command-line
  - system-monitor
---

https://github.com/nicolargo/glances is a cross-platform advance system monitor for usage monitoring for CPU, RAM, Network, GPU, etc.

Install:

=== "Arch Linux"

    ```sh
    sudo pacman -S glances
    ```

=== "pip"

    ```sh
    pip install glances --upgrade --user
    # NVIDIA GPU support
    pip install glances[gpu] --upgrade --user
    ```

=== "Official install script"

    ```sh
    curl -L https://bit.ly/glances | bash
    ```

Usage: call `glances`.
