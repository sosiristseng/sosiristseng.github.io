---
title: Swap Setup
date: 2024-04-22
tags:
  - linux
---

<!-- more -->

## Use a swap file (in btrfs)

Swap files are more flexible than swap partitions in terms of disk space and partition usage.

Source: [btrfs docs](https://btrfs.readthedocs.io/en/latest/Swapfile.html) and [Arch Linux wiki](https://wiki.archlinux.org/title/btrfs#Swap_file).

The following commands create a swapfile in the btrfs filesystem, which does not (and should not) use COW.

```sh
cd /  # Or other dir for the swapfile
sudo mkdir -p /swap
sudo btrfs subvolume create /swap # Create a btrfs subvolume for the swap file
sudo btrfs filesystem mkswapfile --size 4G /swap/swapfile
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

```txt title="/etc/fstab"
/swap/swapfile none swap defaults 0 0
```

And one can see current activated swap by running

```sh
cat /proc/swaps
```

## Use ZRAM

[ZRAM](https://wiki.archlinux.org/title/Zram) is a compressed RAM disk, reducing physical disk swap use under high memory usage.

Install ZRAM in Ubuntu: [Source](https://kienngd.github.io/how-to-use-zram-on-ubuntu-2404/)

```bash
sudo apt update && sudo apt install zram-tools
```

edit `/etc/default/zramswap` to change ZRAM options.

```txt title="/etc/default/zramswap"
ALGO=zstd
PERCENTAGE=50
```
