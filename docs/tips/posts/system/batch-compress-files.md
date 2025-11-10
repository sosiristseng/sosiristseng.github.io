---
title: Batch compress files
date: 2025-11-10
tags:
  - linux
---

Batch compress files with the following tools

- find : https://linux.die.net/man/1/find
- GNU parallel: https://zenodo.org/records/1146014 (PDF) and https://www.gnu.org/software/parallel/parallel_tutorial.html (HTML)
- 7z
- xz

<!-- more -->

## Use XZ to compress all CSV files

```bash
find . -type f -name "*.csv" -print0 | parallel -0 -j32 --progress "xz -z {}"
```

> [!WARNING]
> `xz` removes the original file after compression by default. You can add `-k` option to keep the file.

> [!TIP]
> - Use `--dry-run` before actually running the jobs to ensure the commands are right.
> - Use `-<num>` to change the compression level. For example, `xz -z -9 {}` uses maximum compression.

## Repack all GZ files to XZ ones

```bash
find . -type f -name "*.gz" -print0 | parallel -0 -j32 --progress "zcat {} | xz -z -9 > {.}.xz"
```

## Repack all GZ files to 7Z ones

```bash
find . -type f -name "*.gz" -print0 | parallel -0 -j2 --progress "zcat {} | 7z a -si {.}.7z"
```

## Compress all folders to 7Z

```bash
for f in */; do 7z a "${f%/}.7z" "$f"; done
```

> [!WARNING]
> If you want to use `find` to list all subdirectories, use
> ```bash
> find . -maxdepth 1 -type d -not -path "." | parallel <command>
> ```
> to list every subdirectory and **exclude** the current working directory.
