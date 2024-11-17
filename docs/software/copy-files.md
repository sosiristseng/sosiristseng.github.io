---
title: copy files
tags:
  - ssh
  - linux
  - command-line
  - windows
---

How to copy files with style.

## Use tar

`tar` and pipes can copy file system trees directly, preserving permissions.

```sh
tar cf - $src | tar xvf - -C $dst
```

## Use rsync

```sh
rsync -avh --info=progress2 sourcefolder /destinationfolder --exclude thefoldertoexclude --exclude anotherfoldertoexclude
```

## Copy a directory tree with exclusions

How to exclude some files/folders while copying a folder tree.

### tar

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

### rsync

Use `--exclude` flag in `rsync` to exclude certain folder(s). [^4]

```sh
rsync -avh --progress sourcefolder /destinationfolder --exclude thefoldertoexclude --exclude anotherfoldertoexclude
```

> [!WARNING]
> The excluded directory paths are relative to the *sourcefolder*.

[^4]: https://stackoverflow.com/questions/4585929/how-to-use-cp-command-to-exclude-a-specific-directory


## Copy files over SSH

How to copy files through the secure shell (SSH).

### `scp`

`scp` works similar to the regular copy (`cp`) command.[^scp]

[^scp]: https://kb.iu.edu/d/agye

```sh
scp [options] username1@source_host:directory1/filename1 username2@destination_host:directory2/filename2
```

### `tar`, pipe, and ssh commands

```sh
tar cvf - $localdir | ssh someone@somemachine '(cd destdir && tar xBf -)'
```

### `rsync`

Use a ssh remote as a source or destination folder.

```sh
rsync -avh /source/folder/ username@nasip:dest/folder/
```

### Secure FTP (SFTP)

[Filezilla](https://filezilla-project.org/) and [WinSCP](https://winscp.net/eng/index.php) can access remote servers via the Secure FTP (SFTP) protocol.

### Mount remote directory as a disk via sshfs

https://github.com/libfuse/sshfs mounts a remote machine's directory as a local disk.

```sh
sshfs [user@]hostname:[directory] mount-point
```

To unmount the directory after file operations are done:

```sh
fusermount -u mount-point
```

## Windows CLI tools for copying

- [[robocopy]]
