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

[Bottom](sysmon.md#bottom)

## zoxide

https://github.com/ajeetdsouza/zoxide is a smarter `cd` command that supports all major shells.
