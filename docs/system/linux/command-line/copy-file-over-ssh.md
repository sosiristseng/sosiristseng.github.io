---
title: Copy file over SSH

tags:
  - ssh
  - linux
---

How to copy files through the secure shell (SSH).

## Using `scp` command

`scp` works similar to the regular copy (`cp`) command.[^scp]

[^scp]: https://kb.iu.edu/d/agye

```sh
scp [options] username1@source_host:directory1/filename1 username2@destination_host:directory2/filename2
```

## Using tar, pipe, and ssh commands

```sh
tar cvf - $localdir | ssh someone@somemachine '(cd destdir && tar xBf -)'
```

## Using `rsync` command

```sh
rsync -avh /source/folder/ username@nasip:dest/folder/
```

## Secure FTP (SFTP)

[Filezilla](https://filezilla-project.org/) and [WinSCP](https://winscp.net/eng/index.php) can access remote servers via the Secure FTP (SFTP) protocol.

## Mount remote directory as a disk via sshfs

https://github.com/libfuse/sshfs mounts a remote machine's directory as a local disk.

```sh
sshfs [user@]hostname:[directory] mount-point
```

To unmount the directory after file operations are done:

```sh
fusermount -u mount-point
```
