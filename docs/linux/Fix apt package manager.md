---
title: Fix apt package manager
draft: false
tags:
  - linux/ubuntu
---

Try these commands to fix broken apt package registry (from [system76 docs](https://support.system76.com/articles/package-manager-pop/)).

```sh
sudo apt clean
sudo apt update -m
sudo dpkg --configure -a
sudo apt install -f
sudo apt dist-upgrade
sudo apt autoremove --purge
```