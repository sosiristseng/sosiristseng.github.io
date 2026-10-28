---
title: SSH
tags:
  - command-line
  - linux
  - windows
---

> Tips about the secure shell (SSH)



## Transfer file over ssh

How to copy files through SSH

### tar

```sh
tar cvf - $localdir | ssh someone@somemachine '(cd destdir && tar xBf -)'
```

### rsync

Use a SSH remote as a source or a destination folder.

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
