---
title: Upgrading from ubuntu 22.04 to 24.04
date: 2024-09-03
tags:
  - linux
---

## Before upgrade

- Backup your data.
- Use `ppa-purge` to remove currently activated PPAs. The unremovable `git-lfs` gave me headache for several hours.

<!-- more -->

## Upgrade command

```bash
sudo do-release-upgrade
```

## DNS resolve error

`systemd-resolved` might not be installed after upgrade, to solve the issue:

```bash
sudo apt install systemd-resolved
```

You might need to add an DNS server temporarily to have internet access

```bash
"nameserver 1.1.1.1" >> /etc/resolv.conf
```
