---
title: nohup
tags:
  - linux
  - ssh
---

[nohup](https://cht.sh/nohup) runs background processes uninterruptedly even the remote SSH session goes offline.

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

To monitor what is going on in `nohup.out`

```sh
tail -f nohup.out
```

## End the running process

You can kill the ongoing process by the process ID (PID).

```sh
ps -aux | grep mycmd
kill PID
```

## Run a background process with sudo and nohup

Use `sudo -b CMD`

```sh
nohup sudo -b CMD
```

## Limit the size of nohup.out

Use [logrotate](https://linux.die.net/man/8/logrotate). Configure something like this in `/etc/logrotate.conf`

```txt title="/etc/logrotate.conf"
/path/to/nohup.out {
    size 1024k
    copytruncate
    rotate 100
    maxage 100
}
```
