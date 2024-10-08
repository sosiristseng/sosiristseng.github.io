---
title: Install fonts in Linux
date: 2024-03-25
tags:
  - linux
categories:
  - system
---

Copy the fonts files to `~/.local/share/fonts/`. Then, run `fc-cache` to rebuild fonts cache.

```sh
fc-cache -fv
```
