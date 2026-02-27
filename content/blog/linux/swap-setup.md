---
title: Swap setup
date: 2024-04-22
tags:
  - linux
---

Setup swap spaces.

<!--more-->

## Use a swap file in btrfs

Swap files are more flexible than swap partitions in terms of disk space and partition usage.

Source: [btrfs docs](https://btrfs.readthedocs.io/en/latest/Swapfile.html) and [Arch Linux wiki](https://wiki.archlinux.org/title/btrfs#Swap_file).

The following commands create a swap file in the btrfs filesystem, which does not (and should not) use copy-on-write (COW).

```sh
sudo btrfs subvolume create /swap # Create a btrfs subvolume for the swap file's directory
sudo btrfs filesystem mkswapfile --size 4G --uuid clear /swap/swapfile # Create a 4 GB swap file
sudo swapon /swap/swapfile
```

If `btrfs filesystem mkswapfile` command is not available, use the following command

```sh
cd /swap
sudo truncate -s 0 /swap/swapfile
sudo chattr +C /swap/swapfile
sudo fallocate -l 4G /swap/swapfile
sudo chmod 0600 /swap/swapfile
sudo mkswap /swap/swapfile
sudo swapon /swap/swapfile
```

Add the following line to `/etc/fstab` to mount the swap file on next boot.

```txt {filename="/etc/fstab"}
/swap/swapfile none swap defaults 0 0
```

See the current activated swap file(s):

```sh
cat /proc/swaps
```

## Use ZRAM

[ZRAM](https://wiki.archlinux.org/title/Zram) is a compressed RAM disk, which can be used as a swap device to reduce physical disk swap use under high memory pressure.

Install ZRAM in Ubuntu: [Source](https://kienngd.github.io/how-to-use-zram-on-ubuntu-2404/)

```sh
sudo apt update && sudo apt install zram-tools
```

edit `/etc/default/zramswap` to change the options.

```txt {filename="/etc/default/zramswap"}
ENABLED=true
ALGO=zstd
PERCENTAGE=50
```

enable

```sh
sudo systemctl enable --now zramswap
```

check ZRAM status

```sh
sudo zramctl
```

## Use zswap

[Archwiki: zswap](https://wiki.archlinux.org/title/Zswap)

Zswap is enabled by setting kernel parameters in `/etc/default/grub`

```txt {filename="/etc/default/grub"}
GRUB_CMDLINE_LINUX_DEFAULT="... zswap.enabled=1 zswap.compressor=zstd zswap.zpool=zsmalloc"
```

Run the following to apply changes

```sh
sudo update-grub
```

See the statistics of zswap

```sh
grep -r . /sys/kernel/debug/zswap/
```
