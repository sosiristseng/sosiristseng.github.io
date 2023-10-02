---
title: yt-dlp
tags:
  - multimedia
  - linux
  - windows
---

Install [yt-dlp](https://github.com/yt-dlp/yt-dlp) is an actively developed fork of the famous Youtube video downloader `youtube-dl`.

=== Download executable (Linux/MacOS)

    ```sh
    sudo curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o /usr/local/bin/yt-dlp
    sudo chmod a+rx /usr/local/bin/yt-dlp
    ```

=== Arch Linux

    ```sh
    sudo pacman -S yt-dlp
    ```

=== Windows

    chocolatey

    ```powershell
    choco install yt-dlp
    ```

    winget

    ```powershell
    winget install yt-dlp.yt-dlp
    ```

=== conda

    ```sh
    conda install -c conda-forge yt-dlp
    ```

## Usage

### Download videos with subtitles

Use the `--write-subs` option.

```sh
yt-dlp --write-subs <url>
```

### Limit resolution to 1080

Use `-S` to limit the search range to 1080.

```sh
yt-dlp -S "res:1080" <url>
```

### Download videos from a playlist


```sh
yt-dlp --yes-playlist --ignore-errors --continue --no-overwrites --output "%(title)s.%(ext)s" <playlist_url>
```

- `--yes-playlist` : Download multiple videos if the URL is a playlist.
- `--ignore-errors` : Ignore errors (like geo-restriction of a video or deleted video in a playlist) and continue with rest of the playlist.
- `--continue` : Resume if any of the video is partially downloaded in the local file system.
- `--no-overwrites` : If a file is already downloaded in local file system, then skip the download.
- `--output "%(title)s.%(ext)s` : Specify the download directory with filename and extension extracted from the video.
- `"${VID_URL}"` : URL of the video or playlist.

### Download Watch Later videos and mark them as viewed

Use the `--mark-watched` option. You also need to login with `--usernasme <username> --password <password>`.

```sh
yt-dlp --usernasme <username> --password <password> --mark-watched 'https://www.youtube.com/playlist?list=WL'
```

### Download audio only, as opus format, from a playlist

Use `--extract-audio --audio-format opus --format 'bestaudio'` to extract only the audio information and store as `opus` file.

```sh
yt-dlp --yes-playlist --ignore-errors --continue --no-overwrites --extract-audio --audio-format opus --format 'bestaudio' --output "%(title)s.%(ext)s" "${URL}"
```

### Download videos from a list of videos

Use `--batch-file batchlist.txt` to capture the list of URLs in a separate lines in a text file and download them in batch.

```sh
yt-dlp --ignore-errors --continue --no-overwrites --format 'bestvideo+bestaudio' --batch-file batchlist.txt --output "%(title)s.%(ext)s"
```
