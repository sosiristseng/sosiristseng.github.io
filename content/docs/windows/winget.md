---
title: Winget
tags:
  - windows
---

[winget](https://learn.microsoft.com/zh-tw/windows/package-manager/winget/) is a command-line package manager for Windows.

## winget APPs

- [winget community repository](https://github.com/microsoft/winget-pkgs)
- [winstall](https://winstall.app/)
- [winget.run](https://winget.run/) (Repo archived)

You can also query packages in `winget`

```powershell
winget list [[-q] <query>] [<options>]
```

Install the APP (with admin rights0)

```powershell
winget install -e --id <org.name>
```

- `-e` : requires the exact entry
- `--id <org.name>` : the organization and the name of the APP
