---
title: APT package manager
tags:
  - command-line
  - linux
---

The [APT package manager](https://en.wikipedia.org/wiki/APT_(software)) in Debian, Ubuntu, and derived distributions.

<!--more-->

## `apt` vs `apt-get`

[apt vs apt-get](https://itsfoss.com/apt-vs-apt-get-difference/) from It's FOSS.

- `apt` is for interactive use, including commonly-used commands from `apt-get` and `apt-cache`. And it has a better TUI.
- `apt-get` is more inclined for non-interactive use in scripts because of its stable interface.

## nala: a prettier and faster frontend

[Nala](https://gitlab.com/volian/nala) is a front-end for `libapt-pkg` and is a (almost) drop-in replacement for `apt`.

- Better text UI
- Parallel package downloads
- Discover fastest mirrors (`nala fetch`)

To install `nala`:

```sh
sudo apt install nala
```

To find fastest mirrors:

```sh
sudo nala fetch
```

To update the system:

```sh
sudo nala upgrade
```

## apt-fast: apt in parallel

[apt-fast](https://github.com/ilikenwf/apt-fast) is shell script wrapper for `apt-get` and `aptitude` that can drastically improve `apt` download times by downloading packages in parallel, with multiple connections per package.

One can use `apt-fast` commands just like `apt` e.g., `sudo apt-fast update`, `sudo apt-fast dist-upgrade`.

Should your downloads stall for any reasons, you'll need to run `apt-fast clean` to fix it.

To install `apt-fast`:

```sh
sudo add-apt-repository -y ppa:apt-fast/stable
echo debconf apt-fast/maxdownloads string 16 | sudo debconf-set-selections
echo debconf apt-fast/dlflag boolean true | sudo debconf-set-selections
echo debconf apt-fast/aptmanager string apt-get | sudo debconf-set-selections
sudo apt update && sudo apt install apt-fast -y
```

## Synaptic : the GUI package manager for APT

The additional package `apt-xapian-index` gives a search box in `synaptic`.

```sh
sudo apt install synaptic apt-xapian-index
```

## Fix broken apt

Try these commands to fix broken apt package registry. From [system76 docs](https://support.system76.com/articles/package-manager-pop/).

```sh
sudo apt clean
sudo apt update -m
sudo dpkg --configure -a
sudo apt install -f
sudo apt dist-upgrade
sudo apt autoremove --purge
```
