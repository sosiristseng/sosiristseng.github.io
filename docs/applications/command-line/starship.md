---
title: starship
tags:
  - linux
  - command-line
---

[🚀 Starship command prompt](https://starship.rs/) is an enhancement for command prompt in a multitude of shells, powered by Rust. It is available for `bash`, `zsh`, `fish`, `powershell`, etc.

Install:

=== "Linux/MacOS"

    ```sh
    curl -sS https://starship.rs/install.sh | sh
    ```

=== "Windows"

    ```powershell
    choco install starship
    ```

## Setup

To load starship prompt in the terminal, add the following line(s) at the end.

=== "Bash"

    ```sh title="~/.bashrc"
    eval "$(starship init bash)"
    ```

=== "Zsh"

    ```sh title="~/.zshrc"
    eval "$(starship init zsh)"
    ```

=== "Powershell"

    ```powershell title="Documents\PowerShell\profile.ps1"
    Invoke-Expression (&starship init powershell)
    ```
