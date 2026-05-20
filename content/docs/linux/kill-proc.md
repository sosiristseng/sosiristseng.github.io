---
title: Kill processes in Linux
date: 2024-04-21
tags:
  - linux
---

<!--more-->

## Kill zombie processes

Find and kill zombie process(es). [^1]

```sh
ps axo stat,ppid,pid,comm | grep -w defunct
```

Kill parent process(es)

```sh
sudo kill -9 $ppid
```

## Kill all processes of a user

```sh
sudo pkill -U $UID
```

[^1]: https://wordpress.cine.idv.tw/index.php/2021/02/25/what-to-do-when-ubuntu-displays-there-is-1-zombie-process-upon-login/
