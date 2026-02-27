---
title: Ubuntu postinstall
date: 2024-03-26
tags:
- linux
- postinstall
---

Things to do after installing

- [Ubuntu](https://ubuntu.com/download)
- [Kubuntu](https://kubuntu.org/)
- [WSL2](https://docs.microsoft.com/zh-tw/windows/wsl/install)

<!--more-->

## Make software repo point to NCHC for faster network speed

You can replace `archive.ubuntu.com` with a closer mirror, e.g., `tw.archive.ubuntu.com` or `free.nchc.org.tw` in `/etc/apt/sources.list.d/ubuntu.sources`. After you are done, run:

```sh
sudo apt clean && sudo apt update && sudo apt full-upgrade -y
```

## Install 3rd party apps

First, install required package

```bash
sudo apt update && sudo apt install -y apt-transport-https ca-certificates curl git gnupg-agent software-properties-common
```

- [docker](/docs/software/docker)
- [firefox](/docs/software/firefox)
- [vscode](/docs/software/vscode)
- [cuda](/docs/software/cuda)
- [git](/docs/software/git)

### Brave browser

Setup [Brave browser](https://brave.com)

```sh
sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main" | sudo tee /etc/apt/sources.list.d/brave-browser-release.list > /dev/null
sudo apt update && sudo apt install -y brave-browser
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

### Latest kernel

Install Hardware Enablement (HWE) kernels: https://ubuntu.com/kernel/lifecycle

```sh
sudo apt install --install-recommends linux-generic-hwe-$VERSION
```

Where `$VERSION` is the Ubuntu version.

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

## System tweaks

- [[linux-input-methods]]
- [[linux-themes]]

### Fix locales

Uncomment the `zh_TW` line in `/etc/locale.gen`. Then run:

```sh
sudo locale-gen
```

Finally, install the Traditional Chinese locale in `Language Support` and then set locale to `Taiwan`.

### (Optional) Remove snap

List snap packages

```sh
snap list
```

Uninstall each Snap package

```sh
sudo snap remove --purge $PKG
```

Stop the snapd service and uninstall it

```sh
sudo systemctl stop snapd
sudo apt remove --autoremove --purge snapd
sudo apt-mark hold snapd
```

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

### Disable cloud-init

```sh
sudo touch /etc/cloud/cloud-init.disabled
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

### Making system more responsive

[Fine-tuning the kernel](https://discourse.ubuntu.com/t/fine-tuning-the-ubuntu-24-04-kernel-for-low-latency-throughput-and-power-efficiency/44834)

Replace the line in `/etc/default/grub`

Gaming:

```txt title="/etc/default/grub"
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash preempt=full"
```

Virtualization:

```txt title="/etc/default/grub"
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash preempt=full Nohz_full=all"
```

Then run:

```sh
sudo update-grub
```

## Misc.

- [FreeFileSync](https://freefilesync.org/)
- [Pandoc](https://github.com/jgm/pandoc/releases/)
- [Virtualbox](https://www.virtualbox.org/)
