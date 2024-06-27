---
title: Command Prompt
tags:
  - linux
  - command-line
---

## Bash It

https://github.com/Bash-it/bash-it is the community's collection of useful bash scripts for `bash`, inspired by the [oh-my-zsh](https://ohmyz.sh/) project, providing autocompletion, themes, aliases, custom functions, etc for the bash prompt.

```bash
git clone --depth=1 https://github.com/Bash-it/bash-it.git ~/.bash_it
bash ~/.bash_it/install.sh
```

## Starship

[🚀 Starship command prompt](https://starship.rs/) is an enhancement for command prompt in a multitude of shells, powered by Rust. It is available for `bash`, `zsh`, `fish`, `powershell`, etc.

### Install

=== "Linux/MacOS"

    ```sh
    curl -sS https://starship.rs/install.sh | sh
    ```

=== "Windows"

    ```powershell
    choco install starship
    ```

### Setup

To load starship prompt in the terminal, append the following line(s) to the indicated files.

=== "Bash"

    ```sh title="~/.bashrc"
    eval "$(starship init bash)"
    ```

=== "Zsh"

    ```sh title="~/.zshrc"
    eval "$(starship init zsh)"
    ```

## zimfw

https://github.com/zimfw/zimfw is a blazing fast zsh plugin framework, about 30x faster loading speed than `oh-my-zsh`.

After `zsh` is installed, run:

```sh
wget -nv -O - https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh
```

### Powerlevel10k (p10k) prompt

1. In `~/.zimrc`, replace `zmodule asciiship` with

```sh title="~/.zimrc"
zmodule romkatv/powerlevel10k --use degit
```

2. Run `zimfw install` in zsh to complete install.
3. Install [powerline fonts](https://github.com/romkatv/powerlevel10k#manual) or [nerd fonts](https://www.nerdfonts.com/) for icons.
4. Restart zsh and finish p10k's interactive configuration steps.

### Node version manager (nvm)

1. Add the following line in `~/.zimrc` to add Node version manager (nvm).

```sh title="~/.zimrc"
zmodule lukechilds/zsh-nvm
```

2. Run `zimfw install` in zsh to install nvm.
3. To save loading time of zsh, you can use lazy loading by adding the following line to the beginning of `~/.zshrc`:

```sh title="~/.zshrc"
export NVM_LAZY_LOAD=true
```
