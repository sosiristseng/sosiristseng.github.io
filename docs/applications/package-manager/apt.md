---
title: APT package manager
draft: false
tags:
  - linux/ubuntu
---

APT package manager

- [Itsfoss: apt vs apt-get](https://itsfoss.com/apt-vs-apt-get-difference/)
- [Itsfoss: apt commands](https://itsfoss.com/apt-command-guide/)

**`apt` vs `apt-get`**

- `apt` is for interactive use, including commonly-used commands from `apt-get` and `apt-cache`. And it has a nice progress bar.
- `apt-get` is more inclined for non-interactive (scripting) use due to its stable interface.

## nala: a prettier and faster frontend

[Nala](https://gitlab.com/volian/nala) is a front-end for `libapt-pkg` and is a (almost) drop-in replacement for `apt`.

- Better Text UI
- Parallel package downloads
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

## apt-fast: apt in parallel

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

## Add signing keys

> Use of `apt-key` is deprecated according to the [Debian manpage](https://manpages.debian.org/testing/apt/apt-key.8.en.html)

Here, we take adding signing keys for [[vivaldi]] browser as an example.

```sh
curl -fsSL https://repo.vivaldi.com/archive/linux_signing_key.pub | sudo gpg --dearmor -o /usr/share/keyrings/vivaldi-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/vivaldi-keyring.gpg] https://repo.vivaldi.com/archive/deb/ stable main" | sudo tee /etc/apt/sources.list.d/vivaldi.list > /dev/null
```

- Text key files (`.asc`) should be converted to binary ones (`.gpg`) using `gpg --dearmor`.
- In the apt list, use `[signed-by=/path/to/key.gpg]` to specify the location of the keyring.
- Use `echo <stuff> | sudo tee <file>` to add file content with sudo rights.

## Fix APT package manager

Try these commands to fix broken apt package registry (from [system76 docs](https://support.system76.com/articles/package-manager-pop/)).

```sh
sudo apt clean
sudo apt update -m
sudo dpkg --configure -a
sudo apt install -f
sudo apt dist-upgrade
sudo apt autoremove --purge
```