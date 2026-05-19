---
title: Ibus
tags:
  - input-method
---

[ibus](https://github.com/ibus/ibus) is an input method framework using DBUS. `ibus` integrates better with the GNOME desktop environment.

## Install

```sh
command -v apt && sudo apt install ibus ibus-chewing
command -v pacman && sudo pacman -S ibus ibus-chewing
```

## Setup

If `ibus` does not start on boot, add these lines to `~/.profile` or `~/.profile`.

```sh title=".profile"
export GTK_IM_MODULE=ibus
export QT_IM_MODULE=ibus
export XMODIFIERS=\@im=ibus
ibus-daemon -drx
```
