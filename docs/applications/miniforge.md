---
title: Miniforge
draft: false
tags:
  - python
  - conda
  - linux
  - windows
---

The community-driven [conda-forge](https://conda-forge.org/docs/user/introduction.html) repository with the basic `conda` package manager now includes the fast new [mamba](https://github.com/mamba-org/mamba) package manager.

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
conda install -y conda-libmamba-solver
conda config --set solver libmamba
conda update -y python conda mamba
conda update --all --yes

# `bash` and `zsh` integration
[[ -f ~/.bashrc ]] && conda init bash
[[ -f ~/.zshrc ]] && conda init zsh
```
