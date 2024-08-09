---
title: Development apps
tags:
  - windows
  - bookmark
  - applications
  - git
---

## Git

The famous [Git](https://git-scm.com/) version control system.

chocolatey:

```powershell
choco install git.install
```

winget:

```powershell
winget install Git.Git
```

## GitHub Desktop

[GitHub Desktop](https://desktop.github.com/) is an open source [Electron](https://www.electronjs.org/)-based GitHub app. It is written in [TypeScript](https://www.typescriptlang.org) and uses [React](https://reactjs.org/).

chocolatey:

```powershell
choco install github-desktop
```

winget:

```powershell
winget install -e --id GitHub.GitHubDesktop
```

## VSCode

[Visual Studio Code](https://code.visualstudio.com) is a lightweight but powerful source code editor which runs on your desktop and is available for Linux, macOS and Windows. See also [[vscode]] for more related stuff.

chocolatey:

```powershell
choco install vscode
```

winget:

```powershell
winget install vscode
```

## Hugo

[Hugo](https://gohugo.io/) is the world’s fastest framework for building websites, written in Go. See also [[hugo]] for more related stuff.

chocolatey:

```powershell
choco install hugo-extended
```

Go compiler is needed for Hugo modules

```powershell
choco install golang
```
