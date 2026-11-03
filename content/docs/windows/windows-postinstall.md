---
title: Windows postinstall
tags:
  - windows
---

> Things to do after you install Windows

## MS store for LTSC

In Windows LTSC, run the following command with admin rights and ignore the error. MS store will be installed after a few minutes.

```powershell
wsreset -i
```

And then install the [winget](https://apps.microsoft.com/detail/9nblggh4nns1) package manager.

And then install some packages not shipped with LTSC (with admin rights)

```powershell
winget install 9MVZQVXJBQ9V -s msstore  ## AV1 video extension
winget install 9n4d0msmp0pt -s msstore  ## VP9 video extension
winget install -e --id Microsoft.WindowsTerminal
```

## CTT Windows Utility

The [Chris Titus Tech's Windows Utility](https://github.com/ChrisTitusTech/winutil) provides APP installs, fixes and tweaks.

```powershell
irm "https://christitus.com/win" | iex
```

## Install packages via winget

Install packages via `winget` (with admin rights)

```powershell
winget install -e --id Microsoft.PowerShell --source winget  ## New open-source Powershell
winget install -e --id Daum.PotPlayer --source winget  ## Potplayer
winget install -e --id Git.Git -e --source winget ## Git
winget install -e --id Microsoft.PowerToys ## Power Toys
winget install -e --id Microsoft.VisualStudioCode --override '/SILENT /mergetasks="!runcode,addcontextmenufolders"'
winget install -e --id qBittorrent.qBittorrent
winget install -e --id Mozilla.Firefox
winget install -e --id Brave.Brave
winget install -e --id Telegram.TelegramDesktop
winget install -e --id Bandisoft.Bandizip
winget install -e --id Bandisoft.Honeyview
winget install -e --id M2Team.NanaZip
winget install -e --id yt-dlp.yt-dlp --source winget
winget install -e --id Gyan.FFmpeg
winget install -e --id Nevcairiel.LAVFilters
winget install -e --id CrystalDewWorld.CrystalDiskInfo
winget install -e --id CrystalDewWorld.CrystalDiskMark
winget install -e --id Microsoft.DirectX
winget install -e --id Obsidian.Obsidian
winget install -e --id GitHub.GitHubDesktop
winget install -e --id bDigitalScholar.Zotero
winget install -e --id HandBrake.HandBrake
winget install -e --id=CPUID.CPU-Z
winget install -e --id VideoLAN.VLC
winget install -e --id Microsoft.Coreutils
winget install --id=marlocarlo.pstop
winget install -e --id=astral-sh.uv
winget install -e --id 9NJNWW8PVKMN -s msstore --name Julia
```

## Chocolatey package manager

Install [Chocolatey 🍫](https://chocolatey.org/), a command-line interface (CLI) package manager for Windows.

Run the powershell command with admin rights (e.g. via the `Windows + X` menu):

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

Install packages

```powershell
choco feature enable -n=useRememberedArgumentsForUpgrades
choco install -y nerd-fonts-firacode nerd-fonts-hack
```

See also the [🍫 Chocolatey package list](https://chocolatey.org/packages) for more packages.

## System Tweaks

### Enable `sudo` command

Run the powershell command with admin rights

```powershell
sudo config --enable normal
```

### Disable hibernation

Disabling hibernation saves a lot of disk space (No more `C:\hiberfile.sys`). Run the powershell command with admin rights

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

Or run the following Powershell commands (with admin rights)

```powershell
$path = "HKLM:\SOFTWARE\Microsoft\Windows\Dwm"
New-Item -Path $path -Force | Out-Null
Set-ItemProperty -Path $path -Name "OverlayMinFPS" -Value 0 -Type DWord
Get-ItemProperty -Path $path -Name "OverlayMinFPS"
```

### Fix 'ms-gamingoverlay' link Pop-Up

Save the text below to "fix-gamingoverlay.reg" and double click to apply the registry.

```txt {filename="fix-gamingoverlay.reg"}
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\GameDVR]
"AudioCaptureEnabled"=dword:00000000
"AppCaptureEnabled"=dword:00000000
```

Or run the following Powershell commands (with admin rights)

```powershell
$path = "HKCU:\Software\Microsoft\Windows\CurrentVersion\GameDVR"
New-Item -Path $path -Force | Out-Null
Set-ItemProperty -Path $path -Name "AudioCaptureEnabled" -Value 0 -Type DWord
Set-ItemProperty -Path $path -Name "AppCaptureEnabled" -Value 0 -Type DWord
Get-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\GameDVR" |
    Select-Object AudioCaptureEnabled, AppCaptureEnabled
```

## See also

- Install [WSL](wsl2.md)
