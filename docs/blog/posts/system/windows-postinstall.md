---
title: Windows Postinstall
date: 2024-03-27
tags:
- windows
- postinstall
---

Things to do after Windows install.

See also [The Ultimate Windows Development Environment Guide](https://unicorn-utterances.com/posts/ultimate-windows-development-environment-guide)

## Enable MS store and winget in Windows LTSC

Run the following command in admin rights and ignore the error. MS store will be installed after a few minutes.

```powershell
wsreset -i
```

Click [Microsoft.DesktopAppInstaller](https://apps.microsoft.com/detail/9nblggh4nns1?rtc=1&hl=zh-tw&gl=TW#activetab=pivot:overviewtab) to install winget.

## CTT Windows Utility

The [Chris Titus Tech's Windows Utility](https://github.com/ChrisTitusTech/winutil) provides APP installs, fixes and tweaks.

```powershell
irm christitus.com/win | iex
```

## winget apps

```powershell
winget install Romanitho.Winget-AutoUpdate
winget install Git.Git
winget install Microsoft.WindowsTerminal
winget install Microsoft.PowerShell
winget install Microsoft.VisualStudioCode
winget install qBittorrent.qBittorrent
winget install Mozilla.Firefox
winget install Brave.Brave
winget install Telegram.TelegramDesktop
winget install Bandisoft.Bandizip
winget install M2Team.NanaZip
winget install Bandisoft.Honeyview
winget install Daum.PotPlayer
winget install Nevcairiel.LAVFilters
winget install yt-dlp.yt-dlp
winget install Gyan.FFmpeg
winget install CrystalDewWorld.CrystalDiskInfo
winget install CrystalDewWorld.CrystalDiskMark
winget install Microsoft.DirectX
winget install Starship.Starship
winget install Obsidian.Obsidian
winget install GitHub.GitHubDesktop
```

## Chocolatey package manager

**If winget does not work.**

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

## Afterward

+ Setup [[WSL2]]
+ Setup [[environment-variables]]
