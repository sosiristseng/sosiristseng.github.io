---
title: Rust Tools
tags:
  - linux
  - command-line
  - rust
  - system-monitor
---

See also [rewritten in Rust: Modern Alternatives of Command-Line Tools](https://zaiste.net/posts/shell-commands-rust/)

<!--more-->

## bat : alternative to `cat`

[bat](https://github.com/sharkdp/bat) is a `cat` clone with syntax highlighting and Git integration.

```sh
bat test.md
```

## exa : alternative to `ls`

[exa](https://github.com/ogham/exa) is an improved file lister with more features and better defaults. It uses colours to distinguish file types and metadata. It knows about symlinks, extended attributes, and Git. And it’s small, fast, and just one single binary.

```sh
exa --long --header --git
```

## fd : alternative to `find`

[fd](https://github.com/sharkdp/fd) is a simple, fast and user-friendly alternative to `find`.

```sh
fd PATTERN
```

## ripgrep : alternative to `grep`

[ripgrep](https://github.com/BurntSushi/ripgrep) is a line-oriented search tool that recursively searches the current directory for a regex pattern.

## bottom : alternative to `htop`

[bottom](https://github.com/ClementTsang/bottom) is a cross-platform graphical process/system monitor written in rust.

## zoxide: : alternative to `cd`

[zoxide](https://github.com/ajeetdsouza/zoxide) is a smarter `cd` command that supports all major shells.
