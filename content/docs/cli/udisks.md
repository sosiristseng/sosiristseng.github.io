---
title: udisks
tags:
  - linux
  - command-line
  - system-monitor
  - disks
---

[udisks](https://wiki.archlinux.org/title/Udisks) provides a daemon `udisksd`, that implements D-Bus interfaces used to query and manipulate storage devices, and a command-line tool [udisksctl](https://manpages.ubuntu.com/manpages/noble/man1/udisksctl.1.html), used to query and use the daemon.

To see your drive model:

```bash
udisksctl status
```
