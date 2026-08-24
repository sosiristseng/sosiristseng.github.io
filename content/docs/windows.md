---
title: Windows
tags:
  - windows
---

## Windows post install

### Install software via Chocolatey package manager

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
choco uninstall -n --skipautouninstaller vscode qbittorrent telegram github-desktop brave firefox zotero
```

See also the  [🍫 Chocolatey package list](https://chocolatey.org/packages) for more packages.

## Install software via winget and MS store

In Windows LTSC, run the following command with admin rights and ignore the error. MS store will be installed after a few minutes.

```powershell
wsreset -i
```

- [AV1 video extension](https://apps.microsoft.com/detail/9mvzqvxjbq9v)
- [VP9 video extension](https://apps.microsoft.com/detail/9n4d0msmp0pt)
- [Windows terminal](https://apps.microsoft.com/detail/9n0dx20hk701)
- [Powershell](https://apps.microsoft.com/detail/9mz1snwt0n5d)
- [winget](https://apps.microsoft.com/detail/9nblggh4nns1)
- [PotPlayer](https://potplayer.tv/) can be installed via winget: `winget install -e --id Daum.PotPlayer`
- [PowerShell Core](https://github.com/PowerShell/PowerShell) can be installed [via MS store](https://apps.microsoft.com/detail/9mz1snwt0n5d).
- [Windows terminal](https://github.com/microsoft/terminal) can be installed [via MS store](https://apps.microsoft.com/detail/9n0dx20hk701).

## CTT Windows Utility

The [Chris Titus Tech's Windows Utility](https://github.com/ChrisTitusTech/winutil) provides APP installs, fixes and tweaks.

```powershell
irm "https://christitus.com/win" | iex
```

## Tweaks

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

## See also

See also [The Ultimate Windows Development Environment Guide](https://unicorn-utterances.com/posts/ultimate-windows-development-environment-guide)

## Command line

- [PowerShell Core](https://github.com/PowerShell/PowerShell) can be installed via [MS store](https://apps.microsoft.com/detail/9mz1snwt0n5d).
- [Windows terminal](https://github.com/microsoft/terminal) can be installed via [MS store](https://apps.microsoft.com/detail/9n0dx20hk701).
- [starship](https://starship.rs/) : a cross-shell prompt.
- [Oh My Posh](https://ohmyposh.dev/) : a cross-shell prompt.

## Compression

- [NanaZip](https://github.com/M2Team/NanaZip) : The 7-Zip derivative with Win 11 menu integration. It also has support for Zstandard format. It can be installed via [MS store](https://apps.microsoft.com/detail/9n8g7tscl18r).
- [Peazip](https://github.com/peazip/PeaZip) : Cross-platform file and archive manager.
- [Bandizip](https://en.bandisoft.com/bandizip/): Bandizip is a powerful archiver which provides an ultrafast processing speed and convenient features. It can be installed via [MS store](https://apps.microsoft.com/detail/9p2w3w81sppb).

## Development

- [GitHub Desktop](https://desktop.github.com/): an open source [Electron](https://www.electronjs.org/)-based GitHub app.
- [Visual Studio Code](https://code.visualstudio.com): a lightweight but powerful source code editor available for Linux, macOS and Windows.

## Internet

- [Brave browser](https://brave.com)
- [Firefox browser](https://www.mozilla.org/firefox)
- [Vivaldi browser](https://vivaldi.com/download/)
- [qBittorrent](https://www.qbittorrent.org)
- [Telegram messenger](https://telegram.org)

## Remote desktop

- [Rustdesk](https://rustdesk.com/)

## System tweaks

- [Chris Titus Tech's Windows Utility](https://github.com/ChrisTitusTech/winutil)
- [Dism++](https://github.com/Chuyu-Team/Dism-Multi-language) : Dism Windows image (wim) manipulator and system cleaner.
- [Display Driver Uninstaller (DDU)](https://www.guru3d.com/download/display-driver-uninstaller-download/) : cleanly uninstall NVIDIA/AMD GPU drivers.

### Looks

- [ExplorerPatcher](https://github.com/valinet/ExplorerPatcher) : enhance the working environment on Windows 11.
- [Open Shell Menu](https://github.com/Open-Shell/Open-Shell-Menu) : Classic Shell and startup menu for Windows 10/11.
- [WinSetView](https://lesferch.github.io/WinSetView/) : an easy way to set Windows File Explorer default folder views and disabling annoying groups.

## System information

- [CPU-Z](https://www.cpuid.com/softwares/cpu-z.html)
- [GPU-Z](https://www.techpowerup.com/gpuz/)
- [CrystalDiskInfo](https://crystalmark.info/en/software/crystaldiskinfo/)
- [pstop](https://github.com/psmux/pstop)

## Benchmark

- [CrystalDiskMark](https://crystalmark.info/en/software/crystaldiskmark/) for HDDs/SSDs.
- [Furmark](https://geeks3d.com/furmark/) for GPUs.

## Package manager

- [chocolatey](https://chocolatey.org/) : A Windows package manager.
- [winget](https://github.com/microsoft/winget-cli) : Windows Package Manager CLI (aka winget). The [package repo](https://github.com/microsoft/winget-pkgs). Install it via [MS Store](https://apps.microsoft.com/detail/9nblggh4nns1).

## USB flash drive

- [Rufus](https://rufus.ie/) : Create a bootable USB drive.
- [Ventoy](https://www.ventoy.net/) : Create a bootable USB drive by loading ISO files in the partition.
- [validrive](https://www.grc.com/validrive.htm) : Validate real/fake USB drives. [Youtube video](https://www.youtube.com/watch?v=xMgEHy1A9QA)
