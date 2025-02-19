---
title: Recover Nautilus places folders
date: 2024-03-22
tags:
  - linux
---

How to recover Nautilus (File manager in Gnome) places folders.

<!-- more -->

![](https://user-images.githubusercontent.com/40054455/163508819-5e853b38-4131-44f1-b1ff-5f116d850e17.png)

Check `~/.config/user-dirs.dirs` and make sure the following entries exist and properly setup

```sh title=".config/user-dirs.dirs"
XDG_DESKTOP_DIR="$HOME/Desktop"
XDG_DOWNLOAD_DIR="$HOME/Downloads"
XDG_DOCUMENTS_DIR="$HOME/Documents"
XDG_MUSIC_DIR="$HOME/Music"
XDG_PICTURES_DIR="$HOME/Pictures"
XDG_VIDEOS_DIR="$HOME/Videos"
```

After saving the file, run the following command to reload Nautilus settings:

```sh
xdg-user-dirs-gtk-update
```
