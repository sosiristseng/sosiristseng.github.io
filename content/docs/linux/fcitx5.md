---
title: Fcitx5
tags:
  - input-method
---

[Fcitx](https://wiki.archlinux.org/index.php/Fcitx) is a lightweight input method framework that provides environment-independent language support for Linux. The development energy mainly focuses on the release of the new [version 5](https://wiki.archlinux.org/index.php/Fcitx5).

## Install

```sh
command -v apt && sudo apt install fcitx5 fcitx5-chewing fcitx5-material-color
command -v pacman && sudo pacman -S fcitx5-im fcitx5-chewing fcitx5-material-color
```

## Setup

If `fcitx` does not load on startup, add the following lines to `~/.xprofile` or `~/.profile`.

```sh title="/etc/profile"
export INPUT_METHOD=fcitx5
export GTK_IM_MODULE=fcitx5
export QT_IM_MODULE=fcitx5
export XMODIFIERS=\@im=fcitx5
```
