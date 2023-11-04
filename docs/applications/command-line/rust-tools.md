---
title: Rust Tools
tags:
  - linux
  - command-line
  - rust
  - system-monitor
---

See also [rewritten in Rust: Modern Alternatives of Command-Line Tools](https://zaiste.net/posts/shell-commands-rust/)

## bat : alternative to `cat`

https://github.com/sharkdp/bat is a `cat` clone with syntax highlighting and Git integration.

```sh
bat test.md
```

## exa : alternative to `ls`

https://github.com/ogham/exa is an improved file lister with more features and better defaults. It uses colours to distinguish file types and metadata. It knows about symlinks, extended attributes, and Git. And it’s small, fast, and just one single binary.

```sh
exa --long --header --git
```

## fd : alternative to `find`

https://github.com/sharkdp/fd is a simple, fast and user-friendly alternative to `find`.

```sh
fd PATTERN
```

## ripgrep : alternative to `grep`

https://github.com/BurntSushi/ripgrep is a line-oriented search tool that recursively searches the current directory for a regex pattern.

## Bottom: system monitor written in Rust

https://github.com/clementtsang/bottom is a resource monitor written in Rust.

### Install

#### Ubuntu

Download and install the [deb release](https://github.com/ClementTsang/bottom/releases/latest).

#### Arch Linux

```sh
sudo pacman -S bottom
```

#### snap

```sh
sudo snap install bottom

# To allow the program to run as intended
sudo snap connect bottom:mount-observe
sudo snap connect bottom:hardware-observe
sudo snap connect bottom:system-observe
sudo snap connect bottom:process-control
```

#### Windows

Chocolatey:

```powershell
choco install bottom
```

winget:

```powershell
winget install bottom
```

### Usage

`btm`
