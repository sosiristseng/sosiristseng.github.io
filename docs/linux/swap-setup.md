---
title: Swap Setup
tags:
  - linux
---

## Use Swap file (in btrfs)

Swap file are more flexible in disk space and partition usage than swap partitions.

Source: [btrfs docs](https://btrfs.readthedocs.io/en/latest/Swapfile.html) and [Arch Linux wiki](https://wiki.archlinux.org/title/btrfs#Swap_file).

The swapfile should not use COW.

```sh
cd /  # Or other dir for the swapfile
sudo mkdir -p /swap
sudo btrfs subvolume create /swap # Create a btrfs subvolume for the swap file
sudo btrfs filesystem mkswapfile --size 4G /swap/swapfile
sudo swapon /swap/swapfile
```

Or the following commands if `btrfs filesystem mkswapfile` command is not available.

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

[ZRAM](https://wiki.archlinux.org/title/Zram) is a RAM disk with on-the-fly disk compression, reducing physical disk use under high memory usage.

Install ZRAM in Ubuntu:

```bash
sudo apt install zram-config
```

edit `/usr/bin/init-zram-swapping` to change ZRAM options.
