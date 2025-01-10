---
title: Ubuntu postinstall
tags:
- linux
- postinstall
---

Things to do after installing

- [Ubuntu](https://ubuntu.com/download)
- [Kubuntu](https://kubuntu.org/)
- [WSL2](https://docs.microsoft.com/zh-tw/windows/wsl/install)

> [!INFO]
> How to fix locale:
> Uncomment the `zh_TW` line in `/etc/locale.gen`. And then run:
> ```bash
> sudo locale-gen
> ```
> Finally, install the Traditional Chinese locale in `Language Support` and then set locale to `Taiwan`.

## Make software repo point to NCHC for faster network speed

You can replace  `archive.ubuntu.com` with a closer mirror, e.g., `tw.archive.ubuntu.com` or `free.nchc.org.tw` in `/etc/apt/sources.list.d/ubuntu.sources`. After you are done, run:

```sh
sudo apt clean && sudo apt update && sudo apt full-upgrade -y
```

## (Optional) Remove snap

List snap packages

```sh
snap list
```

Uninstall each Snap package

```sh
sudo snap remove $PKG
```

Stop the snapd service and uninstall it

```sh
sudo systemctl stop snapd
sudo apt remove --autoremove --purge snapd
sudo apt-mark hold snapd
```

## Setup 3rd party apps

Adding 3rd party repositories for latest packages not available in xUbuntu's official repositories.

First, install required package

```bash
sudo apt update && sudo apt install -y apt-transport-https ca-certificates curl git gnupg-agent software-properties-common
```

- [[docker]]
- [[firefox]]
- [[vscode]]

### Brave browser

Setup [Brave browser](https://brave.com)

```sh
sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main" | sudo tee /etc/apt/sources.list.d/brave-browser-release.list > /dev/null
sudo apt update && sudo apt install -y brave-browser
```

### Git

```bash
sudo add-apt-repository -y ppa:git-core/ppa
sudo apt update && sudo apt install -y git git-lfs
```

### qBittorrent

```bash
sudo add-apt-repository -y ppa:qbittorrent-team/qbittorrent-stable
sudo apt update && sudo apt install -y qbittorrent
```

### Telegram messenger

Download and run the [official binaries](https://telegram.org).

### Xanmod Linux kernel

[Xanmod](https://xanmod.org/) is a general-purpose Linux kernel distribution with custom settings and new features.

```bash
curl -fsSL https://dl.xanmod.org/gpg.key | sudo gpg --dearmor -o /usr/share/keyrings/xanmod-keyring.gpg
echo 'deb [signed-by=/usr/share/keyrings/xanmod-keyring.gpg] http://deb.xanmod.org releases main' | sudo tee /etc/apt/sources.list.d/xanmod-kernel.list > /dev/null
sudo apt update && sudo apt install -y linux-xanmod
```

### Nvidia GPU computing (CUDA)

> The following section works for Ubuntu 24.04 LTS.

Install nvidia CUDA runtime and compatible [GPU driver](https://developer.nvidia.com/cuda-downloads).

For Ubuntu 24.04:

```bash
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

For WSL2, install Window NVIDIA GPU driver first; then install the CUDA toolkit in the WSL

```bash
# remove the old GPG key
sudo apt-key del 7fa2af80
# Install Linux CUDA toolkit
wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt update && sudo apt install -y cuda
```

### AMD and Intel open-source GPU library (Mesa)

Install the latest Mesa open source GPU drivers from the [kisak PPA](https://launchpad.net/~kisak/+archive/ubuntu/kisak-mesa)

```bash
sudo add-apt-repository -y ppa:kisak/kisak-mesa
sudo apt update && sudo apt full-upgrade -y
```

### Wine and 32-bit games support

```bash
sudo dpkg --add-architecture i386
```

```bash
sudo mkdir -pm755 /etc/apt/keyrings
sudo wget -O /etc/apt/keyrings/winehq-archive.key https://dl.winehq.org/wine-builds/winehq.key
```

```bash
sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/ubuntu/dists/noble/winehq-noble.sources
sudo apt update && sudo apt install wine
```

### Kubuntu backports

[Kubuntu backports](https://launchpad.net/~kubuntu-ppa/+archive/ubuntu/backports): Latest versions of KDE framework and APPs

```bash
sudo add-apt-repository -y ppa:kubuntu-ppa/backports
sudo apt-get update && sudo apt full-upgrade -y
```

## Update your system and install packages

```sh
sudo apt update && sudo apt full-upgrade -y
```

Ubuntu:

```sh
sudo apt install -y git git-lfs cifs-utils ssh nala gnome-shell-extension-manager parallel baobab ncdu synaptic apt-xapian-index ppa-purge ubuntu-restricted-extras ffmpeg vlc mcomix fonts-wqy-microhei fonts-wqy-zenhei fonts-open-sans ttf-mscorefonts-installer zsh btrfs-compsize
```

Kubuntu:

```sh
sudo apt install -y git git-lfs cifs-utils ssh nala parallel ncdu kio-extras gnome-keyring ppa-purge kubuntu-restricted-extras ffmpeg vlc fonts-wqy-microhei fonts-wqy-zenhei fonts-open-sans ttf-mscorefonts-installer zsh btrfs-compsize synaptic apt-xapian-index
```

## Configurations

### Terminal

- [Nerd fonts](https://www.nerdfonts.com/)
- https://github.com/denysdovhan/one-gnome-terminal : One Dark color theme for gnome-terminal

### Temporary files in RAM disk

Setting `tmpfs` (RAM disk) for `/tmp` folder:

```bash
sudo cp -v /usr/share/systemd/tmp.mount /etc/systemd/system/
sudo systemctl enable tmp.mount
```

### Disable Extended Security Maintenance (ESM)

```bash
sudo mv /etc/apt/apt.conf.d/20apt-esm-hook.conf /etc/apt/apt.conf.d/20apt-esm-hook.conf.disabled
```

### Automatic updates

```bash
sudo apt install unattended-upgrades
sudo dpkg-reconfigure -plow unattended-upgrades
```

### Gnome shell extensions

YOu can also search and install extensions via `gnome-shell-extension-manager`

- [User themes](https://extensions.gnome.org/extension/19/user-themes/)
- [Lock Keys](https://extensions.gnome.org/extension/36/lock-keys/)
- [Applications Menu](https://extensions.gnome.org/extension/6/applications-menu/) : a category-based menu for applications.
- [Dash to panel](https://extensions.gnome.org/extension/1160/dash-to-panel/) : an icon taskbar for Gnome Shell.
- [Arc Menu](https://extensions.gnome.org/extension/3628/arcmenu/) an application menu for GNOME Shell
- [Material shell](https://extensions.gnome.org/extension/3357/material-shell/) tiling windows.

### Kubuntu System Settings

- Double click to open files instead of single clicks: `Workspace behavior` => `General behavior` => `click behavior`.
- Start with an empty session in `Desktop session`.

## Misc.

- [Conda](../software/miniforge.md)
- [[setup-julia]]
- [Linux themes](../software/linux-themes.md)
- [FreeFileSync](https://freefilesync.org/)
- [Hugo](../software/hugo.md)
- [Pandoc](https://github.com/jgm/pandoc/releases/)
- [Virtualbox](https://www.virtualbox.org/)
