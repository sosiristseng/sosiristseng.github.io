---
title: Linux CPU frequency
date: 2024-03-24
tags:
  - linux
  - cpu
categories:
  - system
---

## See current CPU frequency

To display frequencies of all CPU cores every second:

```sh
watch -n1 lscpu --all --extended
```

<!-- more -->

## Change CPU frequency directly

Source: [Stackoverflow](https://askubuntu.com/questions/1415288/how-to-install-cpupower-on-ubuntu-20-04-with-kernel-5-17)

Query CPU options

```sh
grep . /sys/devices/system/cpu/cpu0/cpufreq/*
```

Set the maximum CPU frequency

```sh
echo 4400000 | sudo tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_max_freq
```

##  Change CPU frequency using cpufrequtils

Install `cpufrequtils`

```sh
sudo apt install cpufrequtils
```

Set the maximum CPU frequency

```sh
sudo cpufreq-set -u 4Ghz
```
