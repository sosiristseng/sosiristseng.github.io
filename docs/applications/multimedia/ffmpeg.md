---
title: FFmpeg
tags:
  - multimedia
  - linux
  - windows
---

[ffmpeg](https://ffmpeg.org/ffmpeg-all.html):

## Install

=== "Ubuntu"

    ```sh
    sudo apt install ffmpeg
    ```

=== "Windows"

    chocolatey

    ```powershell
    choco install ffmpeg
    ```

    winget

    ```powershell
    winget install Gyan.FFmpeg
    ```

## Usage

### Simple stream copy

To rebuild "99.9% complete" videos without re-encoding.

```sh
ffmpeg -i input.mkv -c copy -o output.mkv
```
### Remove audio without reencoding video

```sh
ffmpeg -i in.mp4 -vcodec copy -an out.mp4
```

```sh
ffmpeg -i input-video.avi -vn -acodec copy output-audio.aac
```

Options explained:

- `-vn` : no video output.
- `-an` : no audio output.
- `-{a,v}codec copy`: copy without re-encoding.

### Cutting videos

Without re-encoding, just simple copying as-is:

```sh
ffmpeg -i input.mp4 -ss 00:01:00 -to 00:02:00 -c copy output.mp4
```

With re-encoding, slower but more frame accurate:

```sh
ffmpeg -i input.mp4 -ss 00:00:03 -t 00:00:08 -async 1 output.mp4
```

Options explained:
- `-ss` for starting time `hh::mm::ss`
- `-t` for duration of `hh::mm::ss`, or `-to` for end time `hh::mm::ss`
