---
title: GitHub desktop
tags:
  - linux
  - git
  - windows
  - github
---

[GitHub Desktop](https://desktop.github.com/) is an open source [Electron](https://www.electronjs.org/)-based GitHub app. It is written in [TypeScript](https://www.typescriptlang.org) and uses [React](https://reactjs.org/).

## Install

=== "Ubuntu"

    ```bash
    wget -qO - https://apt.packages.shiftkey.dev/gpg.key | gpg --dearmor | sudo tee /usr/share/keyrings/shiftkey-packages.gpg > /dev/null
    sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/shiftkey-packages.gpg] https://apt.packages.shiftkey.dev/ubuntu/ any main" > /etc/apt/sources.list.d/shiftkey-packages.list'
    sudo apt update && sudo apt install github-desktop
    ```

=== "Arch Linux"

    ```bash
    yay -S github-desktop-bin gnome-keyring
    ```

=== "Windows"

    chocolatey:

    ```powershell
    choco install github-desktop
    ```

    winget:

    ```powershell
    winget install -e --id GitHub.GitHubDesktop
    ```
