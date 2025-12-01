---
title: DGX spark postinstall
date: 2015-12-01
tags:
- linux
- postinstall
---

See also [[ubuntu-postinstall]].

## Slim down the system

Manually add required packages first.

```sh
sudo apt install ubuntu-desktop-minimal apturl apturl-common avahi-utils branding-ubuntu dgxstation-desktop dgxstation-grub gnome-tweaks language-pack-en language-pack-gnome-en yaru-theme-unity gedit nautilus-share nvidia-plymouth nvidia-update-manager samba tdb-tools ibus-chewing
```

Then remove unneeded packages, for example:

```sh
sudo apt remove libreoffice
```

The `apt` packages manager will not accidentally remove packages you need due to `nvidia-system-station` dependency.
