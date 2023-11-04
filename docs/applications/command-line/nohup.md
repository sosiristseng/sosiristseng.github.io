---
title: nohup

tags:
  - linux
  - ssh
---

[nohup](https://zh.wikipedia.org/zh-tw/Nohup) runs background process(es) uninterruptedly even the remote SSH session goes offline.

```sh
nohup mycmd &
```

## Output

The output will be in `nohup.out` by default. If you want to customize the output location, just redirect it:

```sh
nohup mycmd &> log.txt &
```

You can also lower the priority for the background process

```sh
nohup nice mycmd &
```

## End the running process

When you're done, you can kill the process by the proccess ID (PID).

```sh
ps -aux | grep mycmd
kill PID
```
