---
title: Fonts Setup
draft:
tags:
  - linux
  - fonts
---

Install custom fonts in Linux systems and make the system recognize it using `fc-cache`.

## Per user

Copy your font files to `~/.local/share/fonts/`. Then, run `fc-cache` to rebuild the font cache.
```sh
fc-cache -fv
```

## System-wide

Copy the font files to `/usr/share/fonts/`. Then, run `fc-cache` with admin rights to rebuild the font cache.
```sh
sudo fc-cache -fv /usr/share/fonts/
```
