---
title: SSH
tags:
  - command-line
  - linux
  - windows
---

> Tips about the secure shell (SSH)

## Install SSH

### Windows

### Linux

## Setup SSH

### Generate a key pair locally (client)

```sh
ssh-keygen -t ed25519 -C "your_email@example.com"
```

The SSH agent will ask you to enter a location to save the keys. e.g. `/home/user/.ssh/id_ed25519`. Passphrase is optional.
Then there will be two SSH key files:

- `~/.ssh/id_ed25519` is the *private key*. **Protect it at all costs.**
- `~/.ssh/id_ed25519.pub` is the *public key*.

> Using different keys for different access points is more secure.

### Accessing the remote machine (server)

Edit `~/.ssh/config`

```sh
mkdir -p ~/.ssh
touch ~/.ssh/config
chmod 600 ~/.ssh/config
nano ~/.ssh/config
```

Add the following content to set the *private key* as the `IdentityFile`.

```txt {filename="~/.ssh/config"}
Host <Your host>
  HostName <remote-ip>
  User <your-name>
  Port <your-port>
  IdentityFile ~/.ssh/id_ed25519
```

### Accessing GitHub repositories via SSH

Edit `~/.ssh/config`

```txt {filename="~/.ssh/config"}
Host GitHub
  HostName github.com
  IdentityFile ~/.ssh/id_ed25519
```

Add the SSH key [here](https://github.com/settings/keys), according to [📖 Github docs](https://docs.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account).

- Paste the content of the *public key*, `~/.ssh/id_ed25519.pub` to the key field.
- Add a descriptive label for the new key in the "Title" field.
- Finally, click the `Add SSH key` green button. If prompted, confirm your GitHub password.

Test your setup, accept its fingerprint if prompted.

```sh
ssh -vT git@github.com
```

Accept its fingerprint if prompted. If you see "Hi user! You've successfully authenticated, but GitHub does not provide shell access" that means login is successful.

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
