---
title: nohup
draft: false
tags:
  - linux
  - ssh
---
[nohup](https://blog.gtwang.org/linux/linux-nohup-command-tutorial/) runs background process(es) uninterruptedly even the remote SSH session becomes offline.[

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

