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

> [!WARNING]
>
>  The default locale in Ubuntu for traditional Chinese (Taiwan) is `lzh_TW` rather than `zh_TW`, which might cause issues. You can change it to `zh_TW` by editing the file `/etc/locale.gen`. Comment out the `lzh_TW` line and uncomment the `zh_TW` line. And then run:
> ```bash
> sudo locale-gen
> ```
> Finally, install the Traditional Chinese locale in `Language Support` and then set locale to `Taiwan` to solve this problem.

## Make software repo point to NCHC for faster network speed

You can replace  `archive.ubuntu.com` with a closer mirror, e.g., `tw.archive.ubuntu.com` or `free.nchc.org.tw` in `/etc/apt/sources.list`. After you are done, run:

```bash
sudo apt clean && sudo apt update && sudo apt full-upgrade -y
```

## Setup 3rd party repos

Adding 3rd party repositories for latest packages not available in xUbuntu's official repositories.

First, install required package

```bash
sudo apt update && sudo apt install -y apt-transport-https ca-certificates curl git gnupg-agent software-properties-common
```

The setup repos for applications:

- [brave](apps/brave.md)
- [docker](apps/docker.md)
- [firefox](apps/firefox.md)
- [git](apps/git.md)
- [qbittorrent](apps/qbittorrent.md)
- [vivaldi](apps/vivaldi.md)
- [vscode](apps/vscode.md)

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

For Ubuntu 22.04:

```bash
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-keyring_1.0-1_all.deb
sudo dpkg -i cuda-keyring_1.0-1_all.deb
sudo apt-get update
sudo apt-get -y install cuda-toolkit
```

To add the CUDA compiler (`nvcc`) to the system `PATH`:

`~/.profile`

```sh
export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```

### AMD and Intel open-source GPU driver (Mesa)

Install the latest Mesa open source GPU drivers from the [kisak PPA](https://launchpad.net/~kisak/+archive/ubuntu/kisak-mesa)

```bash
sudo add-apt-repository -y ppa:kisak/kisak-mesa
sudo apt update && sudo apt full-upgrade -y
```

## (Optional) Wine and 32-bit games support

```bash
sudo dpkg --add-architecture i386
```

## Update your system

```bash
sudo apt update && sudo apt full-upgrade -y
```

## Install apps

### Ubuntu

Save this list as `pkgs.txt`

```txt title="pkgs.txt"
# Development
git
git-lfs

# Network
cifs-utils
deluge
ssh

# System
nala
gnome-shell-extension-manager
parallel
baobab
synaptic
apt-xapian-index
zsh
ppa-purge
libfuse2

# Locale
ibus
ibus-chewing

# Media
ffmpeg
vlc
mcomix
viewnior

# Fonts
fonts-noto
fonts-wqy-microhei
fonts-wqy-zenhei
fonts-open-sans
ttf-mscorefonts-installer
```

### Kubuntu

[Kubuntu backports](https://launchpad.net/~kubuntu-ppa/+archive/ubuntu/backports): Latest versions of KDE framework and APPs

```bash
sudo add-apt-repository -y ppa:kubuntu-ppa/backports
sudo apt-get update && sudo apt full-upgrade -y
```

Save this list as `pkgs.txt`

```txt title="pkgs.txt"
# Development
git
git-lfs

# Network
cifs-utils
qbittorrent
ssh

# System
parallel
zsh
kio-extras
gnome-keyring
kubuntu-restricted-extras
ppa-purge

# Locale
ibus
ibus-chewing

# Media
ffmpeg
smplayer

# Fonts
fonts-noto
fonts-wqy-microhei
fonts-wqy-zenhei
fonts-open-sans
```

### Install packages

Run the following scripts to install packages

```bash
sudo -v
echo ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true | sudo debconf-set-selections
sed 's/#.*$//' pkgs.txt | xargs sudo apt install -y
```

## Configurations

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

### Ubuntu: gnome shell extensions

- [User themes](https://extensions.gnome.org/extension/19/user-themes/)
- [Lock Keys](https://extensions.gnome.org/extension/36/lock-keys/)
- [Applications Menu](https://extensions.gnome.org/extension/6/applications-menu/) : a category-based menu for applications.
- [Dash to panel](https://extensions.gnome.org/extension/1160/dash-to-panel/) : an icon taskbar for Gnome Shell.
- [Arc Menu](https://extensions.gnome.org/extension/3628/arcmenu/) an application menu for GNOME Shell
- [Material shell](https://extensions.gnome.org/extension/3357/material-shell/) tiling windows.

### Kubuntu/KDE Neon: System Settings

- Double click to open files instead of single clicks: `Workspace behavior` => `General behavior` => `click behavior`.
- Start with an empty session in `Desktop session`.

## Misc.

- [Conda](./apps/miniforge.md)
- [[setup-julia]]
- [Linux themes](./apps/linux-themes.md)
- [FreeFileSync](https://freefilesync.org/)
- [Hugo](./apps/hugo.md)
- [Pandoc](https://github.com/jgm/pandoc/releases/)
- [Virtualbox](https://www.virtualbox.org/)
