---
title: Swap Setup
tags:
  - linux
---

## Reduce Swapiness

A low swapiness reduces swap usage and keep more data in RAM.

```sh
echo 'vm.swappiness = 10' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p            
```
you should see 'vm.swappiness = 10'

## Use Swap file

Swap file are more flexible in disk space and partition usage than swap partitions. Ubuntu installations use swap files by default so you don't have to manually enable it. If you want to enable swap file, run the following command:

```sh
# Make a 512 MB swapfile.
sudo dd if=/dev/zero of=/swapfile bs=1M count=512
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

### Swap files in btrfs


### Apply the swap file on next boot

Add the following line to `/etc/fstab`.

```txt title="/etc/fstab"
/swapfile none swap defaults 0 0
```
