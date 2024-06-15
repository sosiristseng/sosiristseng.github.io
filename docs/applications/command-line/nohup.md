---
title: nohup
tags:
  - linux
  - ssh
---

[nohup](https://cht.sh/nohup) runs background process(es) uninterruptedly even the remote SSH session goes offline.

```sh
nohup mycmd &
```

You can also lower the priority for the background process

```sh
nohup nice mycmd &
```

## Output

The output will be in `nohup.out` by default. If you want to customize the output location, just redirect it:

```sh
nohup mycmd &> log.txt &
```

To monitor what is inside `nohup.out`

```sh
tail -f nohup.out
```

## End the running process

When you're done, you can kill the process by the process ID (PID).

```sh
ps -aux | grep mycmd
kill PID
```
