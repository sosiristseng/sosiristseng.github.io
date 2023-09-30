---
title: Copy file over SSH
draft: false
tags:
  - ssh
  - linux
---

How to copy files through the secure shell (SSH).

## scp command

`scp` works similar to regular copy (`cp`) command.[^scp]

[^scp]: https://kb.iu.edu/d/agye

```sh
scp [OPTION] [user@]SRC_HOST:]file1 [user@]DEST_HOST:]file2
```

## tar and pipe

```sh
tar cvf - $localdir | ssh someone@somemachine '(cd somewhere && tar xBf -)'
```
## Secure FTP (SFTP)

[Filezilla](https://filezilla-project.org/) could access remote servers via the Secure FTP (SFTP) protocol.

And newer versions of `scp` also use `sftp` by default.[^scpandsftp]

[^scpandsftp]: https://wiki.archlinux.org/title/SCP_and_SFTP

## Mount as a disk using sshfs

[sshfs](https://github.com/libfuse/sshfs) could mount remote machine's directory as a local disk.

```sh
sshfs [user@]hostname:[directory] mountpoint
```

to unmount the directory

```sh
fusermount -u mountpoint
```

