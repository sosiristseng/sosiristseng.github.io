---
title: Kill processes
date: 2024-04-21
tags:
  - linux
---

## Kill zombie processes

Find and kill zombie process(es). [Source](https://wordpress.cine.idv.tw/index.php/2021/02/25/what-to-do-when-ubuntu-displays-there-is-1-zombie-process-upon-login/)

```bash
ps axo stat,ppid,pid,comm | grep -w defunct
```

Kill parent process(es)

```bash
sudo kill -9 <ppid>
```

## Kill user processes

```bash
sudo pkill -U UID
```
