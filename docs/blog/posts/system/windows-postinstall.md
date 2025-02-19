---
title: Windows Postinstall
date: 2024-03-27
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

## Enable MS store and winget in Windows 10 LTSC 2021

Run the following command and ignore the error. MS store will be installed.

```powershell
wsreset -i
```

Click [Microsoft.DesktopAppInstaller](https://apps.microsoft.com/detail/9nblggh4nns1?rtc=1&hl=zh-tw&gl=TW#activetab=pivot:overviewtab) to install winget.

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

choco install -y vscode qbittorrent firefox brave telegram bandizip nanazip honeyview potplayer lavfilters yt-dlp ffmpeg crystaldiskinfo crystaldiskmark directx vcredist-all sudo starship obsidian nerd-fonts-firacode nerd-fonts-hack github-desktop
choco uninstall -n --skipautouninstaller vscode qbittorrent telegram github-desktop brave
```

See also the  [🍫 Chocolatey package list](https://chocolatey.org/packages) for more packages.

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

## Afterward

+ Setup [[WSL2]]
+ Setup [Environment variables](../../../system/windows-environment-variables.md)
