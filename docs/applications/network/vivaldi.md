---
title: Vivaldi browser
tags:
  - web
  - linux
  - windows
---

[Vivaldi browser](https://vivaldi.com/download/)

## Install

=== "Ubuntu"

    ```bash
    curl -fsSL https://repo.vivaldi.com/archive/linux_signing_key.pub | sudo gpg --dearmor -o /usr/share/keyrings/vivaldi-keyring.gpg
    echo "deb [signed-by=/usr/share/keyrings/vivaldi-keyring.gpg arch=amd64] https://repo.vivaldi.com/archive/deb/ stable main" | sudo tee /etc/apt/sources.list.d/vivaldi.list > /dev/null
    sudo apt update && sudo apt install -y vivaldi-stable
    ```

=== "Windows"

    chocolatey

    ```powershell
    choco install vivaldi
    ```

    winget

    ```powershell
    winget install VivaldiTechnologies.Vivaldi
    ```
