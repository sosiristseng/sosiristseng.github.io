---
title: pacman package manager
tags:
  - linux
---

Managing `pacman` packages in Arch Linux and derivatives (Manjaro, endeavourOS).

## Generating a list of packages

List non-AUR, explicitly installed packages:

```sh
pacman -Qnqe > pkgs.txt
```

List AUR packages:

```sh
pacman -Qqem > aurpkgs.txt
```

List all explicitly installed packages:

```sh
pacman -Qqe > allpkgs.txt
```

## Install packages from a list

```sh
pacman -Syu  # Full upgrade the system first
pacman -S --needed - < pkgs.txt
```

## Arch User Repository (AUR)

The [Arch User Repository (AUR)](https://aur.archlinux.org) hosts community-contributed `PKGBUILD`s, instructions to download and build a packages.

While you could clone the `PKGBUILD` files and run `makepkg -si ` manually, [AUR helpers](https://wiki.archlinux.org/index.php/AUR_helpers) automate these process, giving a similar experience for installing regular packages in `pacman`.

### pikaur

[`pikaur`](https://github.com/actionless/pikaur) reviews PKGBUILDs all in once and asks all questions before installing/building, using systemd dynamic users to spawn build processes.

You can install `pikaur` by another AUR helper, for example:

```sh
yay -S pikaur
```

Afterwards, you can install AUR packages as if installing regular ones

```sh
sudo pikaur -S google-chrome
```

To update all packages

```sh
sudo pikaur -Syu
```

### paru

[`paru`](https://github.com/Morganamilo/paru) is an AUR helper written in Rust.

```sh
yay -S paru-bin # If you don't want to compile the Rust code
# yay -S paru   # Compile paru from source
```

Afterward, you can install AUR packages as if installing regular ones

```sh
paru -S google-chrome
```

To update all packages

```sh
paru
```

### yay

[yay](https://github.com/Jguer/yay) is an AUR helper written in Go and is directly available in Manjaro/EnOS.

You can install AUR packages as if installing regular ones

```sh
yay -S google-chrome
```

To update all packages, just type

```sh
yay
```

Default options for yay could be saved using `yay --save <options>`, for example:

```sh
yay --answerclean All --answerdiff None --answerupgrade None --cleanafter --batchinstall --combinedupgrade --sudoloop --save
```

Explanation:
- `--cleanafter`: clean untracked files after build.
- `--combinedupgrade`: resolve dependency and then install both the repo and the AUR packages in one go.
- `--sudoloop`: Loop sudo calls in the background to prevent sudo from timing out during long builds.
- `--batchinstall`: Build all AUR packages and install them at once.

### Compilation options for AUR packages

To customize compilation options, a good starting point is to copy from the system-wide config file:

```sh
cp /etc/makepkg.conf ~/.makepkg.conf
```

to you own `~/.makepkg.conf` [makepkg@ArchWiki](https://wiki.archlinux.org/index.php/Makepkg). However, `PKGBUILD` settings in the  packages still have higher priorities and can override your settings.

#### CPU target for building optimized binaries

```txt title=".makepkg.conf"
CFLAGS="-march=native -O2 -pipe -fstack-protector-strong -fno-plt"
CXXFLAGS="${CFLAGS}"
RUSTFLAGS="-C opt-level=2 -C target-cpu=native"
```

#### Parallel compilation

```txt title=".makepkg.conf"
MAKEFLAGS="-j$(nproc)"
```

#### Compressing packages

```txt title=".makepkg.conf"
# multiple cores on compression of xz archives
COMPRESSXZ=(xz -c -z - --threads=0)

# multiple cores on compression of zstd archives
COMPRESSZST=(zstd -c -z -q - --threads=0)

# multiple cores on compression of gz archives (requires pigz package)
COMPRESSGZ=(pigz -c -f -n)
```

And you can choose the preferred method for package compression. For example,

```txt title=".makepkg.conf"
PKGEXT='.pkg.tar.zst'
```

Or turn off compression completely (fastest)
```txt title=".makepkg.conf"
PKGEXT='.pkg.tar'
```
