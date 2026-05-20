---
title: zimfw
tags:
  - command-line
  - linux
---

[zimfw](https://github.com/zimfw/zimfw) is a blazing fast zsh plugin framework, about 30x faster loading speed than `oh-my-zsh`.

After `zsh` is installed, run:

```sh
wget -nv -O - https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh
```

## Powerlevel10k (p10k) prompt

1. In `~/.zimrc`, replace `zmodule asciiship` with

```sh {filename="~/.zimrc"}
zmodule romkatv/powerlevel10k --use degit
```

2. Run `zimfw install` in zsh to complete install.
3. Install [powerline fonts](https://github.com/romkatv/powerlevel10k#manual) or [nerd fonts](https://www.nerdfonts.com/) for icons.
4. Restart zsh and finish p10k's interactive configuration steps.

## Node version manager (nvm)

1. Add the following line in `~/.zimrc` to add Node version manager (nvm).

```sh {filename="~/.zimrc"}
zmodule lukechilds/zsh-nvm
```

2. Run `zimfw install` in zsh to install nvm.
3. To save loading time of zsh, you can use lazy loading by adding the following line to the beginning of `~/.zshrc`:

```sh {filename="~/.zshrc"}
export NVM_LAZY_LOAD=true
```
