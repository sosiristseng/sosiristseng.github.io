---
title: coreutils
tags:
  - command-line
  - linux
  - rust
  - windows
---

[GNU `coreutils`](https://en.wikipedia.org/wiki/GNU_Core_Utilities) is a collection of GNU software that implements many standard, Unix-based shell commands.

This article lists some tips about `coreutils`, as well as some alternatives.

## Rust coreutils

[uutils/coreutils](https://github.com/uutils/coreutils) is the Cross-platform Rust rewrite of the GNU `coreutils`.

You can even use them [on Windows](https://learn.microsoft.com/en-us/windows/core-utils/overview). To install with `winget`,

```sh
winget install Microsoft.Coreutils
```

## bat

[bat](https://github.com/sharkdp/bat) is a `cat` clone with syntax highlighting and Git integration.

```sh
bat test.md
```

## dust

[dust](https://github.com/bootandy/dust) is a `du` alternative written in Rust.

```sh
dust $DIR
```

## exa

[exa](https://github.com/ogham/exa) is an improved file lister with more features and better defaults. It uses colors to distinguish file types and metadata. It knows about symlinks, extended attributes, and Git. And it’s small, fast, and just one single binary.

```sh
exa --long --header --git
```

## fd

[fd](https://github.com/sharkdp/fd) is a simple, fast, and user-friendly alternative to `find`.

```sh
fd PATTERN
```

## proc

[proc](https://github.com/dalance/procs) is an `ps` alternative written in Rust.

**Install**

```sh
sudo snap install procs
```

**Usage**

```sh
procs
```

## ripgrep

[ripgrep](https://github.com/BurntSushi/ripgrep) is an alternative to `grep`, a line-oriented search tool that recursively searches the current directory for a regex pattern.

**Install**

```sh
sudo apt install ripgrep
```

**Usage**

See the [user guide](https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md).

## zoxide

[zoxide](https://github.com/ajeetdsouza/zoxide) is a smarter `cd` command that supports all major shells.

**Install**

```sh
curl -sSfL https://raw.githubusercontent.com/ajeetdsouza/zoxide/main/install.sh | sh
```

**Usage**--++-

```sh
z
```
