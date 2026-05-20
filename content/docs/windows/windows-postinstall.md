---
title: Windows Postinstall
date: 2024-03-27
tags:
  - windows
  - postinstall
---

Things to do after Windows install.

<!--more-->

See also [The Ultimate Windows Development Environment Guide](https://unicorn-utterances.com/posts/ultimate-windows-development-environment-guide)

## Install software via Chocolatey package manager

Install [Chocolatey 🍫](https://chocolatey.org/), a command-line interface (CLI) package manager for Windows.

Open the powershell prompt with admin privilege (e.g. via the `Windows + X` menu):

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

Install packages

```powershell
choco feature enable -n=useRememberedArgumentsForUpgrades
choco install -y git.install --params "'/NoShellIntegration'"

choco install -y vscode qbittorrent firefox brave telegram bandizip nanazip honeyview lavfilters yt-dlp ffmpeg crystaldiskinfo crystaldiskmark directx vcredist-all starship obsidian nerd-fonts-firacode nerd-fonts-hack github-desktop zotero handbrake cpu-z gpu-z vlc
choco uninstall -n --skipautouninstaller vscode qbittorrent telegram github-desktop brave firefox
```

See also the  [🍫 Chocolatey package list](https://chocolatey.org/packages) for more packages.

## Other packages

- [PotPlayer](https://potplayer.tv/)
- [PowerShell Core](https://github.com/PowerShell/PowerShell) can be installed [via MS store](https://apps.microsoft.com/detail/9mz1snwt0n5d).
- [Windows terminal](https://github.com/microsoft/terminal) can be installed [via MS store](https://apps.microsoft.com/detail/9n0dx20hk701).

## Tweaks

- [Fix OneDrive issues](onedrive-win.md)

### Enable MS store in LTSC

Run the following command with admin rights and ignore the error. MS store will be installed after a few minutes.

```powershell
wsreset -i
```

Install the packages via the MS store

- [AV1 video extension](https://apps.microsoft.com/detail/9mvzqvxjbq9v)
- [VP9 video extension](https://apps.microsoft.com/detail/9n4d0msmp0pt)
- [Windows terminal](https://apps.microsoft.com/detail/9n0dx20hk701)
- [Powershell](https://apps.microsoft.com/detail/9mz1snwt0n5d)
- [winget](https://apps.microsoft.com/detail/9nblggh4nns1)

### CTT Windows Utility

The [Chris Titus Tech's Windows Utility](https://github.com/ChrisTitusTech/winutil) provides APP installs, fixes and tweaks.

```powershell
irm "https://christitus.com/win" | iex
```

### Disable hibernation

Disabling hibernation saves a lot of disk space (No more `C:\hiberfile.sys`). Run this in powershell with admin rights:

```powershell
powercfg -h off
```

### Fix Chromium rendering issue

From this [reddit thread](https://www.reddit.com/r/Windows11/comments/1kgp7ar/cause_and_solution_to_windows_24h2_related/).

> Some people may have noticed after the windows 11 24H2 update that they began to experience issues with electron/chromium based apps(Discord, VSCode, Chrome itself) when being alt-tabbed out of a game.
> Frequently, it will appear as if only parts of the interface are being updated, maybe you scrolling down a chat, but only a third of it is scrolling and the rest appears frozen in place.

Save and double click this registry file.

```txt {filename="dwm_mpo_fix.reg"}
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Dwm]
"OverlayMinFPS"=dword:00000000
```

### Fix 'ms-gamingoverlay' link Pop-Up

Save the text below to "fix-gamingoverlay.reg" and double click to apply the registry.

```txt {filename="fix-gamingoverlay.reg"}
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\GameDVR]
"AudioCaptureEnabled"=dword:00000000
"AppCaptureEnabled"=dword:00000000
```
