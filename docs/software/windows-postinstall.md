---
title: Windows Postinstall
date: 2024-03-27
tags:
- windows
- postinstall
---

Things to do after Windows install.

See also
- [The Ultimate Windows Development Environment Guide](https://unicorn-utterances.com/posts/ultimate-windows-development-environment-guide)

## Install software

See also: [[windows-tools]]

### Enable MS store and winget

> For Windows LTSC versions

Run the following command with admin rights and ignore the error. MS store will be installed after a few minutes.

```powershell
wsreset -i
```

### Install via MS store

Packages in MS store: https://apps.microsoft.com/search

- [AV1 video extension](https://apps.microsoft.com/detail/9mvzqvxjbq9v)
- [VP9 video extension](https://apps.microsoft.com/detail/9n4d0msmp0pt)
- [Windows terminal](https://apps.microsoft.com/detail/9n0dx20hk701)
- [Powershell](https://apps.microsoft.com/detail/9mz1snwt0n5d)
- [winget](https://apps.microsoft.com/detail/9nblggh4nns1)

### Install via Chocolatey package manager

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

choco install -y vscode qbittorrent firefox brave telegram bandizip nanazip honeyview potplayer lavfilters yt-dlp ffmpeg crystaldiskinfo crystaldiskmark directx vcredist-all starship obsidian nerd-fonts-firacode nerd-fonts-hack github-desktop zotero handbrake cpu-z gpu-z
choco uninstall -n --skipautouninstaller vscode qbittorrent telegram github-desktop brave firefox
```

See also the  [🍫 Chocolatey package list](https://chocolatey.org/packages) for more packages.

## Tweaks

- [[WSL2|Set up WSL2]]
- [[environment-variables| Set environment variables]]
- [[developement/julia|Setup Julia]]

### CTT Windows Utility

The [Chris Titus Tech's Windows Utility](https://github.com/ChrisTitusTech/winutil) provides APP installs, fixes and tweaks.

```powershell
irm christitus.com/win | iex
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

``` title="dwm_mpo_fix.reg"
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Dwm]
"OverlayMinFPS"=dword:00000000
```

### Windows LTSC fixes

Run the following command with admin rights to restore MS store.

```powershell
wsreset -i
```

Apply the following registry to fix OneDrive in the Explorer. [^fix-onedrive]

```txt title="fix-onedrive.reg"
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{A52BBA46-E9E1-435f-B3D9-28DAA648C0F6}]
"Attributes"=dword:00000001
"Category"=dword:00000004
"DefinitionFlags"=dword:00000040
"Icon"=hex(2):25,00,53,00,79,00,73,00,74,00,65,00,6d,00,52,00,6f,00,6f,00,74,\
  00,25,00,5c,00,73,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,00,5c,00,69,00,\
  6d,00,61,00,67,00,65,00,72,00,65,00,73,00,2e,00,64,00,6c,00,6c,00,2c,00,2d,\
  00,31,00,30,00,34,00,30,00,00,00
"LocalizedName"=hex(2):40,00,25,00,53,00,79,00,73,00,74,00,65,00,6d,00,52,00,\
  6f,00,6f,00,74,00,25,00,5c,00,53,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,\
  00,5c,00,53,00,65,00,74,00,74,00,69,00,6e,00,67,00,53,00,79,00,6e,00,63,00,\
  43,00,6f,00,72,00,65,00,2e,00,64,00,6c,00,6c,00,2c,00,2d,00,31,00,30,00,32,\
  00,34,00,00,00
"LocalRedirectOnly"=dword:00000001
"Name"="OneDrive"
"ParentFolder"="{5E6C858F-0E22-4760-9AFE-EA3317B67173}"
"ParsingName"="shell:::{018D5C66-4533-4307-9B53-224DE2ED1FE6}"
"RelativePath"="OneDrive"

[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{A52BBA46-E9E1-435f-B3D9-28DAA648C0F6}]
"Attributes"=dword:00000001
"Category"=dword:00000004
"DefinitionFlags"=dword:00000040
"Icon"=hex(2):25,00,53,00,79,00,73,00,74,00,65,00,6d,00,52,00,6f,00,6f,00,74,\
  00,25,00,5c,00,73,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,00,5c,00,69,00,\
  00,31,00,30,00,34,00,30,00,00,00
"LocalizedName"=hex(2):40,00,25,00,53,00,79,00,73,00,74,00,65,00,6d,00,52,00,\
  6f,00,6f,00,74,00,25,00,5c,00,53,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,\
  00,5c,00,53,00,65,00,74,00,74,00,69,00,6e,00,67,00,53,00,79,00,6e,00,63,00,\
  43,00,6f,00,72,00,65,00,2e,00,64,00,6c,00,6c,00,2c,00,2d,00,31,00,30,00,32,\
  00,34,00,00,00
"LocalRedirectOnly"=dword:00000001
"Name"="OneDrive"
"ParentFolder"="{5E6C858F-0E22-4760-9AFE-EA3317B67173}"
"ParsingName"="shell:::{018D5C66-4533-4307-9B53-224DE2ED1FE6}"
"RelativePath"="OneDrive"
```

[^fix-onedrive]: https://ibug.io/blog/2025/04/windows-10-ltsc-onedrive-explorer-sidebar-fix/
