---
title: Change user directory
date: 2025-01-10
tags:
  - linux
---

Use `sudo` and `at` to schedule the `usermod` command, which changes the user's home dir.

```bash
sudo at "now +5 minutes"  # Run the following commands in 5 minutes
```

In the `at` interface

```bash
pkill -u UID            # kill user processes
usermod -m -d /new/home # Change user home dir (-d) and move (-m) the content into the new folder
```

`Ctrl+D` to exit the `at` interface. Logout, wait 10 minutes, and login.

## See also

- [at](https://linux.die.net/man/1/at)
- [usermod](https://linux.die.net/man/8/usermod)
- [pkill](https://linux.die.net/man/1/pkill)
