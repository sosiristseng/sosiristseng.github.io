---
title: Power limit for nvidia GPUs
draft: false
tags:
  - linux
  - gpu
---

Source: [Puget systems](https://www.pugetsystems.com/labs/hpc/quad-rtx3090-gpu-power-limiting-with-systemd-and-nvidia-smi-1983/)

```bash
# Enable persistence mode
sudo nvidia-smi -pm 1

# Power limit to 300 Watt
sudo nvidia-smi -pl 300
```

To monitor GPU power draw:

```bash
nvidia-smi -q -d POWER -l 1 | grep "Power Draw"
```
