---
title: CUDA
date: 2025-02-20
tags:
- linux
- gpu
---

*For Ubuntu 24.04*

Clean previous installations

```bash
sudo apt autopurge 'cuda*' 'nvidia*'
```

Install nvidia CUDA runtime and compatible GPU driver from NVIDIA: https://developer.nvidia.com/cuda-toolkit

```sh
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt update && sudo apt -y install cuda-toolkit-12-9
```

Add the CUDA compiler (`nvcc`) to the system `PATH`:

```sh title="~/.profile"
export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}
```

For WSL2, install Windows NVIDIA GPU driver first; then install the CUDA toolkit in the WSL.

```sh
sudo apt-key del 7fa2af80 # remove the old GPG key
# Install Linux CUDA toolkit
wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt update && sudo apt install -y cuda
```
