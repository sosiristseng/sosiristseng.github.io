---
title: Ubuntu postinstall
tags:
- linux/ubuntu
- postinstall
---

Things to do after installing

- [Ubuntu](https://ubuntu.com/download)
- [Kubuntu](https://kubuntu.org/)
- [WSL2](https://docs.microsoft.com/zh-tw/windows/wsl/install)

> [!warning]
> The default locale in Ubuntu for traditional Chinese (Taiwan) is `lzh_TW` rather than `zh_TW`, which might cause issues. You can change it to `zh_TW` by editing the file `/etc/locale.gen`. Comment out the `lzh_TW` line and uncomment the `zh_TW` line. And then run:
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

[[ubuntu-3rd-party]]

## (Optional) Wine and 32-bit games support

```bash
sudo dpkg --add-architecture i386
```

## Update your system

```bash
sudo apt update && sudo apt full-upgrade -y
```

## Install apps

### Regular Ubuntu

Save this list as `pkgs.txt`

```txt title="pkgs.txt"
# Developement
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

Save this list as `pkgs.txt`

```txt title="pkgs.txt"
# Developement
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

## Other configurations

- [[swap-setup]] configuration
- [[linux-input-methods]] setup
- [[fonts-setup]]
- Setting [[environment-variables]]
- [[linux-themes]] setup
- Set [[linux-local-time]] if you are dual booting with Windows.

### Ubuntu: Extensions for gnome shell

- [User themes](https://extensions.gnome.org/extension/19/user-themes/)
- [Audio Output Switcher](https://extensions.gnome.org/extension/751/audio-output-switcher/)
- [Audio Selector](https://extensions.gnome.org/extension/5135/audio-selector/)
- [Lock Keys](https://extensions.gnome.org/extension/36/lock-keys/)
- [Applications Menu](https://extensions.gnome.org/extension/6/applications-menu/) for a category-based menu for applications.
- [Dash to panel](https://extensions.gnome.org/extension/1160/dash-to-panel/) : an icon taskbar for Gnome Shell.
- [Arc Menu](https://extensions.gnome.org/extension/3628/arcmenu/) an application menu for GNOME Shell
- [Material shell](https://extensions.gnome.org/extension/3357/material-shell/) tiling windows.
### Kubuntu/KDE Neon: System Settings

- Double click to open files instead of single clicks: `Workspace behavior` => `General behavior` => `click behavior`.
- Start with an empty session in `Desktop session`.

## Other apps if needed

- [[mambaforge]]
- [[setup-julia]]
- [FreeFileSync](https://freefilesync.org/)
- [Starship](https://starship.rs/)
- [Hugo](https://github.com/gohugoio/hugo/releases/)
- [Pandoc](https://github.com/jgm/pandoc/releases/)
- [Virtualbox](https://www.virtualbox.org/)
