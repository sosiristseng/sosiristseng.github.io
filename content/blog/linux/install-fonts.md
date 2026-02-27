---
title: Install fonts in Linux
tags:
  - linux
---

Copy the fonts files to `~/.local/share/fonts/`. Then, run `fc-cache` to rebuild fonts cache.

```sh
fc-cache -fv
```
