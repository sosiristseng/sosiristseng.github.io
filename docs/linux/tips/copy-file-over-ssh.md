---
title: Copy file over SSH

tags:
  - ssh
  - linux
---

How to copy files through the secure shell (SSH).

## Using scp command

`scp` works similar to the regular copy (`cp`) command.[^scp]

[^scp]: https://kb.iu.edu/d/agye

```sh
scp [options] username1@source_host:directory1/filename1 username2@destination_host:directory2/filename2
```

## Using tar and pipe

```sh
tar cvf - $localdir | ssh someone@somemachine '(cd destdir && tar xBf -)'
```

## Secure FTP (SFTP)

[Filezilla](https://filezilla-project.org/) could access remote servers via the Secure FTP (SFTP) protocol.

And newer versions of `scp` also use `sftp` by default.[^scpandsftp]

[^scpandsftp]: https://wiki.archlinux.org/title/SCP_and_SFTP

## Mount remote directory as a disk via sshfs

https://github.com/libfuse/sshfs mounts a remote machine's directory as a local disk.

```sh
sshfs [user@]hostname:[directory] mountpoint
```

To unmount the directory after file operations are done:

```sh
fusermount -u mountpoint
```
