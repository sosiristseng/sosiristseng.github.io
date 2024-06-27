---
title: Manual
date: 2023-08-27
tags:
  - linux
  - command-line
---

Alternatives to the [man](https://linux.die.net/man/) command:

## cheat.sh

[cheat.sh](https://cheat.sh/) is an online cheat sheet that can be accessed via the browser and the `curl` command.

For example,

```sh
curl cht.sh/tar
```

## tldr

https://github.com/tldr-pages/tldr are collaborative cheat sheets for console commands, a complement to `man` pages. They are also available as [a PDF document](https://tldr.sh/assets/tldr-book.pdf)

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
