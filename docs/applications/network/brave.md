---
title: Brave Browser
tags:
  - web
  - linux
  - windows
---

Setup [Brave browser](https://brave.com)

Install:

=== "Ubuntu"

    ```sh
    sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
    echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main" | sudo tee /etc/apt/sources.list.d/brave-browser-release.list > /dev/null
    sudo apt update && sudo apt install -y brave-browser
    ```

=== "Arch Linux"

    ```sh
    yay -S brave-bin
    ```

=== Windows

    chocolatey:

    ```powershell
    choco install brave
    ```

    winget:

    ```powershell
    winget install Brave.Brave
    ```
