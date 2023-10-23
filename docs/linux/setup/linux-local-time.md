---
title: Linux local time

tags:
  - linux
---

One might want to set cllock to local time zone in Linux (which follows universal time by default) to show correct time when dual booting Linux and Windows systems.[^1]


```bash
timedatectl set-local-rtc 1
```

[^1]: https://itsfoss.com/wrong-time-dual-boot/
