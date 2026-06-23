---
title: ffmpeg
tags:
  - cli
  - multimedia
---

Setup [ffmpeg](https://ffmpeg.org). See also [Arch Wiki: ffmpeg](https://wiki.archlinux.org/title/FFmpeg)

<!--more-->

## Install

### Ubuntu

```sh
sudo apt install ffmpeg
```

### Windows

```powershell
choco install ffmpeg
```

Or

```powershell
winget install Gyan.FFmpeg
```

## Usage

### Simple stream copy

To rebuild "99.9% complete" videos without re-encoding.

```sh
ffmpeg -i input.mkv -c copy -o output.mkv
```
### Remove audio without re-encoding video

```sh
ffmpeg -i in.mp4 -c:v copy -an out.mp4
```

```sh
ffmpeg -i input-video.avi -vn -c:a copy output-audio.aac
```

Options explained:

- `-vn` : no video output.
- `-an` : no audio output.
- `-{a,v}codec copy`: copy without re-encoding.

### Cutting videos

Without re-encoding, just simple copying as-is:

```sh
ffmpeg -ss 00:01:00 -i input.mp4 -t 00:01:00 -c copy output.mp4
```

With re-encoding, slower but more frame accurate:

```sh
ffmpeg -ss 00:00:03 -i input.mp4 -t 00:00:08 -async 1 output.mp4
```

Options explained:

- `-ss` for seeking to starting time `hh:mm:ss`.
- `-t` for the duration of `hh:mm:ss`, or `-to` for the end time `hh:mm:ss`.
