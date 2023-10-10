---
title: Ubuntu 3rd party repositories
tags:
- linux/ubuntu
---

Adding 3rd party repositories for latest packages not available in xUbuntu's official repositories.

First, install required package

```bash
sudo apt update && sudo apt install -y apt-transport-https ca-certificates curl git gnupg-agent software-properties-common
```

## Kubuntu APP and KDE framework updates

[Kubuntu backports](https://launchpad.net/~kubuntu-ppa/+archive/ubuntu/backports): Latest versions of KDE framework and APPs

```bash
sudo add-apt-repository -y ppa:kubuntu-ppa/backports
sudo apt-get update && sudo apt full-upgrade -y
```

## Apps

- [[apt#apt-fast apt but faster|apt-fast]]
- [[brave]]
- [[docker]]
- [[git]]
- [[qbittorrent]]
- [[vivaldi]]
- [[vscode]]

## Drivers

### Xanmod Linux kernel

[Xanmod](https://xanmod.org/) is a general-purpose Linux kernel distribution with custom settings and new features.

```bash
curl -fsSL https://dl.xanmod.org/gpg.key | sudo gpg --dearmor -o /usr/share/keyrings/xanmod-keyring.gpg
echo 'deb [signed-by=/usr/share/keyrings/xanmod-keyring.gpg] http://deb.xanmod.org releases main' | sudo tee /etc/apt/sources.list.d/xanmod-kernel.list > /dev/null
sudo apt update && sudo apt install -y linux-xanmod
```

### Nvidia GPU computing (CUDA)

> The following section works for Ubuntu 22.04 LTS.

Install nvidia CUDA runtime and compatible [GPU driver](https://developer.nvidia.com/cuda-downloads).

```bash
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-keyring_1.0-1_all.deb
sudo dpkg -i cuda-keyring_1.0-1_all.deb
sudo apt-get update
sudo apt-get -y install cuda
```

### AMD and Intel open-source GPU driver (Mesa)

Install the latest Mesa open source GPU drivers from the [kisak PPA](https://launchpad.net/~kisak/+archive/ubuntu/kisak-mesa)

```bash
sudo add-apt-repository -y ppa:kisak/kisak-mesa
sudo apt update && sudo apt full-upgrade -y
```

## Themes

Setup [[linux-themes]].
