---
title: Git
tags:
  - git
  - linux
  - windows
---

- [Git reference](https://git-scm.com/docs)
- [Git cheat sheet (pdf)](https://training.github.com/downloads/github-git-cheat-sheet.pdf)
- [When you screw up git](https://ohshitgit.com/)

## Install

=== "Windows"

```powershell
choco feature enable -n=useRememberedArgumentsForUpgrades
choco install -y git.install --params "'/NoShellIntegration'"
```

=== "Ubuntu"

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

```title=".gitattributes"
* text=auto eol=lf
```

Apply the changes

```bash
git add --renormalize .
```
