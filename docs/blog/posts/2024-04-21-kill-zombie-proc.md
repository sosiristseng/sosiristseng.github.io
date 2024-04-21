---
title: Kill zombie processes
date: 2024-04-21
tags:
  - linux
---

[Source](https://wordpress.cine.idv.tw/index.php/2021/02/25/what-to-do-when-ubuntu-displays-there-is-1-zombie-process-upon-login/)

Find zombie process(es)

```bash
ps axo stat,ppid,pid,comm | grep -w defunct
```

Kill parent process(es)

```bash
sudo kill -9 <ppid>
```
