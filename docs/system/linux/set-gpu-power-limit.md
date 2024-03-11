---
title: Power limit for nvidia GPUs

tags:
  - linux
  - gpu
---

You can make GPUs consume less (or more) power by setting the power limit.

Source: [Puget systems](https://www.pugetsystems.com/labs/hpc/quad-rtx3090-gpu-power-limiting-with-systemd-and-nvidia-smi-1983/)

```bash
# Power limit to 300 Watt
sudo nvidia-smi -pl 300
```

To monitor GPU power draw:

```bash
nvidia-smi -q -d POWER -l 1 | grep "Power Draw"
```
