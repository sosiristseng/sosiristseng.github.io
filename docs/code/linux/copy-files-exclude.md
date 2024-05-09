---
title: Copy a directory tree with exclusions
tags:
  - linux
---

How to exclude some files/folders while copying a folder tree.

## Tar

To start with, `tar` and pipes can be used to copy directly trees[^1]

```sh
tar cf - $src | tar xvf - -C $dst
```

[^1]: https://docstore.mik.ua/orelly/unix3/upt/ch10_13.htm

A filter file `.tarignore` excludes stuff similar to `.gitignore`.[^2][^3]

```sh
tar -c -X .tarignore -f - srcfolder | tar xvf - -C dstfolder
```

The syntax is similar to `.gitignore`:

```txt title=".tarignore"
.DS_Store
.git
.gitignore
```

[^2]: https://stackoverflow.com/questions/39514510/exclude-directories-from-tar-archive-with-a-tarignore-file
[^3]: https://www.gnu.org/software/tar/manual/html_node/exclude.html#index-exclude_002dignore

## rsync

Use `--exclude` flag in `rsync` to exclude certain folder(s). [^4]

```sh
rsync -av --progress sourcefolder /destinationfolder --exclude thefoldertoexclude --exclude anotherfoldertoexclude
```

> [!WARNING]
> The excluded directory paths are relative to the *sourcefolder*.

[^4]: https://stackoverflow.com/questions/4585929/how-to-use-cp-command-to-exclude-a-specific-directory
