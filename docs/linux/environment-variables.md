---
title: Linux environment variables
tags:
  - linux
---

[Arch Wiki: environment variables](https://wiki.archlinux.org/index.php/environment_variables)

## System-wide

+ `/etc/profile` is sourced by all POSIX-compatible shells upon login.
+ Files inside the `/etc/profile.d/` directory will also be sourced.

## Bash

+ `~/.profile` or `~/.bash_profile` for login bash instances.
+ `~/.bashrc` for every interactive bash instance.

## Zsh

+ `~/.zshenv` for environment variables in all zsh instances.
+ `~/.zprofile` for every login zsh instance.
+ `~/.zshrc` for every interactive zsh instance.

>[!NOTE]
> zsh [does not source](https://superuser.com/questions/187639/zsh-not-hitting-profile) `~/.profile` by default because of the difference between bash and zsh syntaxes. You can add this line to `~/.zprofile` or `~/.zshenv` to make zsh shells read `~/.profile correctly.
> ```zsh title="~/.zshenv"
> skip_global_compinit=1
> test -r ${HOME}/.profile && emulate sh -c 'source ${HOME}/.profile'
> ```

## X Window

+ `~/.xinitrc` is sourced by `startx`.
+ `~/.xprofile` is sourced by display managers (e.g., GDM, SDDM)

## Systemd and Wayland

+ `~/.config/environment.d/*.conf`: sourced by `systemd`. Also, they are used in Wayland sessions where `xinitrc` and `xprofile` are not available.
