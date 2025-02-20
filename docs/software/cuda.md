---
title: CUDA
date: 2025-02-20
tags:
- linux
- gpu
---

Install nvidia CUDA runtime and compatible [GPU driver](https://developer.nvidia.com/cuda-downloads).

## From ubuntu repository

## From NVIDIA (newer driver and CUDA runtime)

For Ubuntu 24.04:

```sh
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/cuda-ubuntu2404.pin
sudo mv cuda-ubuntu2404.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/12.6.0/local_installers/cuda-repo-ubuntu2404-12-6-local_12.6.0-560.28.03-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2404-12-6-local_12.6.0-560.28.03-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2404-12-6-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda
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
