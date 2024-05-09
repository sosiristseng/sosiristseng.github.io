---
title: Windows Postinstall
tags:
- windows
- postinstall
---

Things to do after Windows install.

See also [The Ultimate Windows Development Environment Guide](https://unicorn-utterances.com/posts/ultimate-windows-development-environment-guide)

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

choco install -y winget-cli vscode qbittorrent firefox brave vivaldi telegram bandizip nanazip honeyview potplayer lavfilters yt-dlp ffmpeg crystaldiskinfo crystaldiskmark directx vcredist-all sudo starship obsidian nerd-fonts-firacode nerd-fonts-hack github-desktop tabby winscp
```

See also the  [🍫 Chocolatey package list](https://chocolatey.org/packages) for more packages.

## CTT Windows Utility

The [Chris Titus Tech's Windows Utility](https://github.com/ChrisTitusTech/winutil) provides APP installs, fixes and tweaks.

```powershell
irm christitus.com/win | iex
```

## Disable hibernation

Disabling hibernation saves a lot of disk space (No more `C:\hiberfile.sys`). Run this in powershell with admin rights:

```powershell
powercfg -h off
```

## (Optional) Compress OS files for a smaller disk space footprint

```powershell
Compact.exe /CompactOS:always
```

## Install nvidia GPU driver

You can use [nvcleaninstall](https://www.techpowerup.com/download/techpowerup-nvcleanstall/) to install Nvidia driver without bloat.

## Others

+ Setup [[WSL2]]
