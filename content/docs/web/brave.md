---
title: Brave Browser
tags:
  - web
---

## Install Brave

**Windows**

```powershell
winget install --id Brave.Brave -e
```

**Linux**

Install Brave origin

```sh
curl -fsS https://dl.brave.com/install.sh | FLAVOR=origin sh
```

## Move Brave's user and cache folder

**Windows**

1. Close the brave browser
2. Move this folder to a new location: `%LOCALAPPDATA%\BraveSoftware\Brave-Browser\User Data`
3. Run `cmd` as the administrator and run the following command to make a symbolic link to the new location

> Make sure the target path R:\BraveUserData exists and that the User Data folder doesn't already exist (move/back it up first, since Brave must be closed).

```
mklink /D "%LOCALAPPDATA%\BraveSoftware\Brave-Browser\User Data\" "R:\BraveUserData"
```

Or powershell as the administrator

```powershell
New-Item -ItemType SymbolicLink -Path "$env:LOCALAPPDATA\BraveSoftware\Brave-Browser\User Data" -Target "R:\BraveUserData"
```

4. You will see a folder with a small arrow if it works.
