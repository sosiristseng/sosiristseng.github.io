---
title: Git
tags:
  - linux
  - git
  - windows
---

The famous [Git](https://git-scm.com/) version control system.

- [Git commands](../../../code/git/index.md)
- [Git operations in GitHub actions](../../../code/github-actions/list-of-github-actions/git-ops-gha.md)

## Install

=== "Ubuntu"

    ```bash
    sudo add-apt-repository -y ppa:git-core/ppa
    sudo apt update && sudo apt install -y git git-lfs
    ```

=== "Arch Linux"

    ```sh
    sudo pacman -S git git-lfs
    ```

=== "Windows"

    chocolatey:

    ```powershell
    choco install git.install
    ```

    winget:

    ```powershell
    winget install Git.Git
    ```
