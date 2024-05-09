---
title: Manual
date: 2023-08-27
tags:
  - linux
  - command-line
---

Besides using [man](https://linux.die.net/man/) to find usage for commands, one can use the following tools.

## cheat.sh

[cheat.sh](https://cheat.sh/) is an online cheat sheet that can be accessed via the browser and the `curl` command.

For example,

```sh
curl cht.sh/tar~list
```

returns

```sh
# cheat:tar
# To list the content of an .tgz or .tar.gz archive:
tar -tzvf /path/to/foo.tgz
tar -tzvf /path/to/foo.tar.gz

# To list the content of an .tar.bz2 archive:
tar -tjvf /path/to/foo.tar.bz2

# cheat:tarsnap
# List the archives
tarsnap --list-archives

# tldr:tart
# List VMs:
tart list
```

## tldr

https://github.com/tldr-pages/tldr are collaborative cheat sheets for console commands, a complement to `man` pages. They are also available as [a pdf document](https://tldr.sh/assets/tldr-book.pdf)

### Install

=== "npm"

    ```sh
    npm install -g tldr
    ```

=== "pip"

    ```sh
    pip install --user -U tldr
    ```

### Usage

To see examples of the `tar` command, type:

```sh
tldr tar
```
