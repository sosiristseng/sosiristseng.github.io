---
title: micromamba
tags:
  - python
---

[`micromamba`](https://mamba.readthedocs.io/en/latest/user_guide/micromamba.html) is a fully statically-linked, self-contained, package manager for conda environments.

## Installation

Windows:

```powershell
Invoke-Expression ((Invoke-WebRequest -Uri https://micro.mamba.pm/install.ps1 -UseBasicParsing).Content)
```

Linux:

```sh
"${SHELL}" <(curl -L micro.mamba.pm/install.sh)
```

## Update micromamba

```sh
micromamba self-update
```

## Commands

`micromamba` shares the same commands as `conda` and `mamba` package managers.

### Create an environment

To create an environment:

```sh
micromamba create -n $name ${packages}
```

To create an environment from a spec file

```sh
micromamba create -n $name -f $envfile
```

To create an environment at a specific folder

```sh
micromamba create -p $dirpath ${packages}
```

### Activate an environment

To activate an environment:

```sh
micromamba activate $name
```

To run a command from an environment

```sh
micromamba run -n $name $cmd
```

Or

```sh
micromamba run -p $dirpath $cmd
```
