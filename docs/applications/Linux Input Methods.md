---
title: Linux Input Methods
tags:
  - linux
  - apps
---

Input methods enable multilingual inputs including CJK (Chinese, Japanese, Korean).

## Fcitx5

[Fcitx](https://wiki.archlinux.org/index.php/Fcitx) is a lightweight input method framework aimed at providing environment independent language support for Linux. The development energy is mainly focused on the new [version 5](https://wiki.archlinux.org/index.php/Fcitx5) release.

To install:

```bash
[[ -x $(command -v pacman) ]] && sudo pacman -S fcitx5-im fcitx5-chewing fcitx5-material-color
[[ -x $(command -v apt) ]]    && sudo apt install fcitx5 fcitx5-chewing fcitx5-material-color
```

Add the following lines to `/etc/profile` if `fcitx` does not load on startup.

```sh title="/etc/profile"
export INPUT_METHOD=fcitx5
export GTK_IM_MODULE=fcitx5
export QT_IM_MODULE=fcitx5
export XMODIFIERS=\@im=fcitx5
```

## Ibus

[ibus](https://github.com/ibus/ibus) is an input method framework using DBUS. `ibus` integrates better with the GNOME desktop environment.

To install:

```bash
[[ -x $(command -v pacman) ]] && sudo pacman -S ibus ibus-chewing
[[ -x $(command -v apt) ]]    && sudo apt install ibus ibus-chewing
```

If `ibus` does not start automatically at login, add these lines to `~/.xprofile` or `~/.profile` to load ibus at login.

```sh title=".xprofile"
export GTK_IM_MODULE=ibus
export QT_IM_MODULE=ibus
export XMODIFIERS=\@im=ibus
ibus-daemon -drx
```
