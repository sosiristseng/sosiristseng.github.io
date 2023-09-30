---
title: starship
tags:
- apps
- linux
- command-line
---

[🚀 Starship command prompt](https://starship.rs/) is an enhancement for command prompt in a multitude of shells, powered by Rust. It is available for `bash`, `zsh`, `fish`, `powershell`, etc.

## Install
Installation from the [offical documentation](https://starship.rs/guide/#%F0%9F%9A%80-installation):
### Linux/MacOS

```sh
curl -sS https://starship.rs/install.sh | sh
```

### Windows

```powershell
choco install starship
```

## Setup

To load starship prompt, add the following line at the end of respective files.

### Bash
```sh title="~/.bashrc"
eval "$(starship init bash)"
```

### Zsh
```sh title="~/.zshrc"
eval "$(starship init zsh)"
```

### Powershell
```powershell title="Documents\PowerShell\profile.ps1"
Invoke-Expression (&starship init powershell)
```