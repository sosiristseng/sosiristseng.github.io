---
title: Text mode at boot
date: 2025-11-30
tags:
  - linux
---

<!--more-->

```sh
sudo systemctl set-default multi-user.target
sudo reboot
```

Source: https://www.baeldung.com/linux/boot-linux-command-line-mode

To switch back to GUI mode at boot:

```sh
sudo systemctl set-default graphical.target
sudo reboot
```

What are the "targets"?

Source: https://unix.stackexchange.com/questions/404667/systemd-service-what-is-multi-user-target

```
Run Lvl Target Units                        Description
0       runlevel0.target, poweroff.target   Shut down and power off
1       runlevel1.target, rescue.target     Set up a rescue shell
2,3,4   runlevel[234].target,               Set up a non-gfx multi-user shell
        multi-user.target
5       runlevel5.target, graphical.target  Set up a gfx multi-user shell
6       runlevel6.target, reboot.target     Shut down and reboot the system
```
