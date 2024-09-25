---
title: tmux
tags:
  - command-line
  - linux
  - ssh
---

[ Arch Wiki: tmux](https://wiki.archlinux.org/title/Tmux)

[tmux](https://github.com/tmux/tmux) is a terminal multiplexer: it enables a number of terminals to be created, accessed, and controlled from a single screen. tmux may be detached from a screen and continue running in the background, then later reattached. For example, it enables programs run uninterrupted via ssh since ssh connects the screen while the program run in the background.

## Install (Ubuntu)

`tmux` is usually preinstalled. In case it's not, run:

```sh
sudo apt install tmux
```

## Setup

The configuration file is `~/.tmux.conf`

```txt title="~/.tmux.conf"
# Enable mouse scroll
set -g mouse
# Multicolor terminal
set -g default-terminal "screen-256color"
```

See also [Oh my tmux](https://github.com/gpakosz/.tmux), a versatile tmux configuration tool.