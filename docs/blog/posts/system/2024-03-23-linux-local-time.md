---
title: Use local time in Linux
date: 2024-03-23
tags:
  - linux
categories:
  - system
---

When dual-booting Linux and Windows,it might be better to set the clock to the local time zone in Linux[^localtime] to in sync with Windows settings.

```bash
timedatectl set-local-rtc 1
```

[^localtime]: https://itsfoss.com/wrong-time-dual-boot/
