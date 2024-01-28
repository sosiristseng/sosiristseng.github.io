---
title: glances
tags:
  - linux
  - command-line
  - system-monitor
---

https://github.com/nicolargo/glances is a cross-platform advance system monitor for usage monitoring for CPU, RAM, Network, GPU, etc.

## Install

Official install script

```sh
curl -L https://bit.ly/glances | bash
```

Or

```sh
wget -O- https://bit.ly/glances | bash
```

### Arch Linux

```sh
sudo pacman -S glances
```

### Ubuntu: pip

```sh
sudo apt update && sudo apt install python3-psutil

pip install glances --upgrade --user
# NVIDIA GPU support
pip install glances[gpu] --upgrade --user
```

## Usage

Enter `glances` in the terminal.
