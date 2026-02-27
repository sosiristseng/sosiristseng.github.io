---
title: Move Linux user directory
date: 2025-01-10
tags:
  - linux
---

Use the [`usermod` command](https://linux.die.net/man/8/usermod) to move one user's home dir.

<!--more-->

Login as another user with `sudo` rights.

```bash
sudo pkill -u $USER                # kill user processes
sudo usermod -m -d /new/home $USER # Change user home dir (-d) and move (-m) the content into the new folder
```
