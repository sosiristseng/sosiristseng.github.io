---
title: APT package manager
draft: false
tags:
- apps
- linux/ubuntu
---

APT package manager

- [Itsfoss: apt vs apt-get](https://itsfoss.com/apt-vs-apt-get-difference/)
- [Itsfoss: apt commands](https://itsfoss.com/apt-command-guide/)

**`apt` vs `apt-get`**

- `apt` is for interactive use, including commonly-used commands from `apt-get` and `apt-cache`. And it has a nice progress bar.
- `apt-get` is more inclined for non-interactive (scripting) use due to its stable interface.

## nala: apt but neater

[Nala](https://gitlab.com/volian/nala) is a front-end for `libapt-pkg` and is a (almost) drop-in replacement for `apt`.

- Better Text UI
- Parallel package download
- Discover fastest mirrors (`nala fetch`)

To install `nala`:

```sh
sudo apt install nala
```

To find fasterst mirrors:

```sh
sudo nala fetch
```

To upgrade the system:

```sh
sudo nala upgrade
```

## apt-fast: apt but faster

[apt-fast](https://github.com/ilikenwf/apt-fast) is shellscript wrapper for `apt-get` and `aptitude` that can drastically improve `apt` download times by downloading packages in parallel, with multiple connections per package.

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

```sh
sudo apt install synaptic apt-xapian-index
```

The additional package `apt-xapian-index` offers a quick search box in `synaptic`.

## Tips

- [[Fix apt package manager]]
- [[Add signing keys to apt]]