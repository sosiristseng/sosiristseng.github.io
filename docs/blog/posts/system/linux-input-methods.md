---
title: Linux Input Methods
date: 2025-02-19
tags:
  - linux
---

Input methods enable multilingual inputs, including CJK (Chinese, Japanese, and Korean).

## Fcitx5

[Fcitx](https://wiki.archlinux.org/index.php/Fcitx) is a lightweight input method framework that provides environment-independent language support for Linux. The development energy mainly focuses on the release of the new [version 5](https://wiki.archlinux.org/index.php/Fcitx5).

### Install

```bash
command -v apt && sudo apt install fcitx5 fcitx5-chewing fcitx5-material-color
command -v pacman && sudo pacman -S fcitx5-im fcitx5-chewing fcitx5-material-color
```

### Setup

Add the following lines to `~/.xprofile` or `~/.profile` if `fcitx` does not load on startup.

```sh title="/etc/profile"
export INPUT_METHOD=fcitx5
export GTK_IM_MODULE=fcitx5
export QT_IM_MODULE=fcitx5
export XMODIFIERS=\@im=fcitx5
```

## Ibus

[ibus](https://github.com/ibus/ibus) is an input method framework using DBUS. `ibus` integrates better with the GNOME desktop environment.

### Install

```bash
command -v apt && sudo apt install ibus ibus-chewing
command -v pacman && sudo pacman -S ibus ibus-chewing
```

### Setup

Add these lines to `~/.xprofile` or `~/.profile` if `ibus` does not load on startup.

```sh title=".xprofile"
export GTK_IM_MODULE=ibus
export QT_IM_MODULE=ibus
export XMODIFIERS=\@im=ibus
ibus-daemon -drx
```
