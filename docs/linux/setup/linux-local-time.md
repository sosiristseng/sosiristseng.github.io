---
title: Linux local time
tags:
  - linux
---

When dual-booting Linux and Windows, one might want to set the clock to the local time zone in Linux, which follows universal time (UTC) by default.[^1]

```bash
timedatectl set-local-rtc 1
```

[^1]: https://itsfoss.com/wrong-time-dual-boot/
