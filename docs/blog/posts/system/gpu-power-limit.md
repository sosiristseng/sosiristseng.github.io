---
title: Power limit for nvidia GPUs
date: 2024-03-20
tags:
  - linux
  - gpu
---

You can make GPUs consume less (or more) power by setting the power limit.

Source: [Puget systems](https://www.pugetsystems.com/labs/hpc/quad-rtx3090-gpu-power-limiting-with-systemd-and-nvidia-smi-1983/)

<!-- more -->

To limit power draw to 300W:
```bash
sudo nvidia-smi -pl 300
```

To monitor GPU power draw:
```bash
nvidia-smi -q -d POWER -l 1 | grep "Power Draw"
```
