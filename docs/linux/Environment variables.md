---
title: Environment variables
tags:
  - windows
  - linux
draft:
---

## Linux

[Arch Wiki: environment variables](https://wiki.archlinux.org/index.php/environment_variables)

### System-wide

- `/etc/profile` is sourced by all POSIX-compatible shells upon login.
- Files inside the `/etc/profile.d/` directory will also be sourced.

### Bash

- `~/.profile` or `~/.bash_profile` for login bash shells.
- `~/.bashrc` for every bash (interactive shell) instance.

### Zsh

- `~/.zshenv` for environment variables in zsh.
- `~/.zprofile` for login zsh shells.
- `~/.zshrc` for every zsh (interactive shell) instance.

> [!note]
> zsh [does not read](https://superuser.com/questions/187639/zsh-not-hitting-profile) `~/.profile` by default. You can add this line to `~/.zprofile` or `~/.zshenv` to let zsh login shells read `~/.profile`

```zsh
[[ -r ~/.profile ]] && emulate sh -c 'source ~/.profile'
```

### X windows

- `~/.xinitrc` is sourced by `startx`.
- `~/.xprofile` is sourced by display managers (e.g. GDM, SDDM)

### Systemd

- `~/.config/environment.d/*.conf`: sourced by `systemd`. Used in WayLand sessions where `xinitrc` and `xprofile` is not available.

## Windows

[Environment variables in Powershell](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_environment_variables?view=powershell-7.3)

### Shell variables

Variables created by `set` are bound to the current session and not persistent.

```powershell
$Env:FOO = "example"
$Env:FOO
```

### Persistent variables

- GUI: Windows Settings -> Advanced system settings -> Set **Environment Variables**.
- CLI: `SetEnvironmentVariable` function.

```powershell
[Environment]::SetEnvironmentVariable('Foo', 'Bar', 'Machine')
```
