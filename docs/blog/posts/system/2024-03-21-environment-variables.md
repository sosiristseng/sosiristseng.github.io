---
title: Environment variables
date: 2024-03-21
tags:
  - linux
  - windows
categories:
  - system
---

## Linux environment variables

[Arch Wiki: environment variables](https://wiki.archlinux.org/index.php/environment_variables)

### System-wide

+ `/etc/profile` is sourced by all POSIX-compatible shells upon login.
+ Files inside the `/etc/profile.d/` directory will also be read.

### Bash

+ `~/.profile` or `~/.bash_profile` for login bash instances.
+ `~/.bashrc` for every interactive bash instance.

### Zsh

+ `~/.zshenv` for environment variables in all zsh instances.
+ `~/.zprofile` for every login zsh instance.
+ `~/.zshrc` for every interactive zsh instance.

>[!NOTE]
> zsh [does not source](https://superuser.com/questions/187639/zsh-not-hitting-profile) `~/.profile` by default because of the difference between bash and zsh syntaxes. You can add this line to `~/.zprofile` or `~/.zshenv` to make zsh shells read `~/.profile correctly.
> ```zsh title="~/.zshenv"
> skip_global_compinit=1
> test -r ${HOME}/.profile && emulate sh -c 'source ${HOME}/.profile'
> ```

### X Window

+ `~/.xinitrc` is sourced by `startx`.
+ `~/.xprofile` is sourced by display managers (e.g., GDM, SDDM)

### Systemd and Wayland

+ `~/.config/environment.d/*.conf`: sourced by `systemd`. Also, they are used in Wayland sessions where `xinitrc` and `xprofile` files are not available.


## Windows environment variables

[Environment variables in Powershell](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_environment_variables?view=powershell-7.3)

### Session variables

Variables created by `set` are bound to the current session and not persistent.

```powershell
$Env:FOO = "example"
$Env:FOO
```

### Persistent variables

+ GUI: Windows Settings -> Advanced system settings -> Set **Environment Variables**.
+ Powershell: `[Environment]::SetEnvironmentVariable('KEY', 'VAL', 'Machine')`
+ Cmd: `SETX KEY VAL`
