---
title: Miniforge
draft: false
tags:
  - python
  - conda
  - linux
  - windows
---

The community-driven [conda-forge](https://conda-forge.org/docs/user/introduction.html) repo with fast new [mamba](https://github.com/mamba-org/mamba) package manager. Now `miniforge` also includes the `mamba` package manager.

## Windows

Download and run the installer from the [miniforge GitHub repo](https://github.com/conda-forge/miniforge#download).

## Linux

Download and install the Miniforge installer in Linux.

```bash
CONDA_PATH="${HOME}/conda"
CONDA_SH="${CONDA_PATH}/etc/profile.d/conda.sh"
CONDA_URL="https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh"

# Download and install miniconda/mambaforge
wget -O /tmp/conda.sh "${CONDA_URL}"
bash /tmp/conda.sh -bup "${CONDA_PATH}"
source "${CONDA_SH}"
conda activate base

# conda package manager setup
# conda config --set auto_activate_base false
conda config --set default_threads $(nproc)
mamba update python conda --yes
mamba update --all --yes

# `bash` and `zsh` integration
[[ -f ~/.bashrc ]] && conda init bash
[[ -f ~/.zshrc ]] && conda init zsh
```
