---
title: cheat.sh
date: 2023-08-27
tags:
  - linux
  - command-line
---

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
