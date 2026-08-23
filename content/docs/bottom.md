---
title: Bottom
tags:
  - command-line
  - system-monitor
  - linux
---

[bottom](https://github.com/ClementTsang/bottom) is a cross-platform graphical process and system monitor written in Rust.

See the [instructions](https://github.com/ClementTsang/bottom#installation) in the README.

```sh
sudo snap install bottom

# To allow the program to run as intended
sudo snap connect bottom:mount-observe
sudo snap connect bottom:hardware-observe
sudo snap connect bottom:system-observe
sudo snap connect bottom:process-control
```

Usage

```sh
btm
```
