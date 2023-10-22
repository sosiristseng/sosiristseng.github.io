---
title: Set CPU frequency
tags:
  - linux
---

## Changing the settings directly

From the [Stackoverflow post](https://askubuntu.com/questions/1415288/how-to-install-cpupower-on-ubuntu-20-04-with-kernel-5-17)

Query CPU options

```bash
grep . /sys/devices/system/cpu/cpu0/cpufreq/*
```

Set the maximum CPU frequency

```bash
echo 4400000 | sudo tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_max_freq
```

## cpufrequtils

You can also install the tool `cpufrequtils`

```bash
sudo apt install cpufrequtils
```

Set the maximum CPU frequency

```bash
sudo cpufreq-set -u 4Ghz
```
