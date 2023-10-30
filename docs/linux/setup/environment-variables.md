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
+`~/.zshrc` for every interactive zsh instance.

!!! note
    zsh [does not source](https://superuser.com/questions/187639/zsh-not-hitting-profile) `~/.profile` by default. You can add this line to `~/.zprofile` or `~/.zshenv` to let zsh login shells read `~/.profile`

    ```zsh title="~/.zshenv"
    test -r ${HOME}/.profile && emulate sh -c 'source ${HOME}/.profile'
    ```

## X Window

+ `~/.xinitrc` is sourced by `startx`.
+ `~/.xprofile` is sourced by display managers (e.g. GDM, SDDM)

## Systemd and WayLand

+ `~/.config/environment.d/*.conf`: sourced by `systemd`. Also they are used in WayLand sessions where `xinitrc` and `xprofile` are not available.


## See also

[[windows/environment-variables|Windows environment variables]]
