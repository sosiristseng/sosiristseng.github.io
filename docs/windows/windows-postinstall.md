---
title: Windows Postinstall
tags:
- windows
- postinstall
---

Things to do after Windows install.

See also [The Ultimate Windows Development Environment Guide](https://unicorn-utterances.com/posts/ultimate-windows-development-environment-guide)

## CTT Windows Utility

The [Chris Titus Tech's Windows Utility](https://github.com/ChrisTitusTech/winutil) provides APP installs, fixes and tweaks.

```powershell
irm christitus.com/win | iex
```

## Chocolatey package manager

Install [Chocolatey 🍫](https://chocolatey.org/), a command-line interface (CLI) package manager for Windows.

Open the powershell prompt with admin privilege (e.g. via the `Windows + X` menu):

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

Install packages

```powershell
choco feature enable -n=useRememberedArgumentsForUpgrades

choco install -y git.install --params "'/NoShellIntegration'"

choco install -y vscode qbittorrent firefox brave telegram bandizip honeyview potplayer lavfilters yt-dlp ffmpeg crystaldiskinfo directx vcredist-all hugo-extended sudo starship obsidian nerd-fonts-firacode nerd-fonts-hack github-desktop tabby
```

See the  [🍫 Chocolatey package list](https://chocolatey.org/packages) for more packages.

### Install winget in Windows LTSC

```powershell
choco install -y winget-cli
```

## Disable hibernation

Disabling hibernation saves a lot of disk space (No more `C:\hiberfile.sys`). Run this in powershell in admin mode:

```pwsh
powercfg -h off
```

## More

+ Setup [[WSL2]].
+ Setup [[windows/environment-variables]].
