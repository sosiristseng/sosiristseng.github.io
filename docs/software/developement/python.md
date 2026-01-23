---
title: Python package manager
tags:
  - python
  - conda
  - linux
  - windows
---

## miniforge

https://github.com/conda-forge/miniforge is a Python distribution that uses
- community-driven [conda-forge](https://conda-forge.org/docs/user/introduction.html) repository
- basic `conda` package manager and the fast new [mamba](https://github.com/mamba-org/mamba) package manager.

Installation

=== "Windows"

    Download and run the installer in https://github.com/conda-forge/miniforge

=== "Linux"

    ```bash
    CONDA_PATH="${HOME}/conda"
    CONDA_SH="${CONDA_PATH}/etc/profile.d/conda.sh"
    CONDA_URL="https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh"

    # Download and install
    wget -O /tmp/conda.sh "${CONDA_URL}"
    bash /tmp/conda.sh -bup "${CONDA_PATH}"
    source "${CONDA_SH}"
    conda activate base

    # conda package manager setup
    conda config --set auto_activate_base false
    conda config --set default_threads $(nproc)
    conda update python --yes && conda update --all --yes

    # `bash` and `zsh` integration
    conda init bash || true
    conda init zsh || true
    ```

## micromamba

`micromamba` is a fully statically-linked, self-contained, executable for conda environments.

### Installation

=== "Windows"

    ```powershell
    Invoke-Expression ((Invoke-WebRequest -Uri https://micro.mamba.pm/install.ps1 -UseBasicParsing).Content)
    ```

=== "Linux"

    ```sh
    "${SHELL}" <(curl -L micro.mamba.pm/install.sh)
    ```

### Update

```sh
micromamba self-update
```

### Commands

`micromamba` has no "base" environment. Other than that, it shares basically the same commands as `conda` and `mamba`.

To create an environment:

```sh
micromamba create -n <name> <list of packages>
```

To create an environment from a spec file

```sh
micromamba create -n <name> -f <envfile>
```

To install an environment to a specific folder

```sh
micromamba create -p <dirpath> <list of packages>
```

To activate an environment:

```sh
micromamba activate <name>
```

To run a command from an environment

```sh
micromamba run -n <name> <command>
```

Or

```sh
micromamba run -p <dirpath> <command>
```
