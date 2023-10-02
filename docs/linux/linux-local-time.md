---
title: Linux local time
draft: false
tags:
  - linux
---

One might want to set cllock to local time zone in Linux (which follows universal time by default) to show correct time when dual booting Linux and Windows systems. From [It's FOSS](https://itsfoss.com/wrong-time-dual-boot/).

```bash
timedatectl set-local-rtc 1
```
