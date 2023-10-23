---
title: Git
tags:
  - linux
  - git
  - windows
---

About the [Git](https://git-scm.com/) version control system.

Install git

=== "Ubuntu"

    ```bash
    sudo add-apt-repository -y ppa:git-core/ppa
    sudo apt update && sudo apt install -y git git-lfs
    ```

=== "Arch Linux"

    ```sh
    pacman -S git git-lfs
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

## Git tips

- [[git/index|Git commands]]
- [[git-ops-gha|Git operations in GitHub actions]]
