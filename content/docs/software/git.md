---
title: Git
tags:
  - git
  - linux
  - windows
  - development
---

Setup [Git](https://git-scm.com/) version control.

<!--more-->

## Install

### Windows

```powershell
choco feature enable -n=useRememberedArgumentsForUpgrades
choco install -y git.install --params "'/NoShellIntegration'"
```

### Ubuntu

```bash
sudo add-apt-repository -y ppa:git-core/ppa
sudo apt update && sudo apt install -y git git-lfs
```

## Settings

### Let Windows use `LF` end of line:

```bash
# Default is true on Windows machines
git config --global core.autocrlf input
```

You might want to add a `<repo>/.gitattributes` file in the repo to enforce the setting.

```txt {filename=".gitattributes"}
* text=auto eol=lf
```

Apply the changes

```bash
git add --renormalize .
```
