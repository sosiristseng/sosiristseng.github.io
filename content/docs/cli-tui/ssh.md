---
title: SSH
tags:
  - command-line
  - linux
  - windows
---

> Tips about the secure shell (SSH)

## Install SSH

Both SSH server and client

**Windows**

Check if SSH components are installed.

```powershell
Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'
```

Run the following command in Powershell as the administrator to install SSH components and start the service.

```powershell
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
Start-Service sshd
Set-Service -Name sshd -StartupType 'Automatic'
```

Verify the firewall rule

```powershell
Get-NetFirewallRule -Name *ssh*
```

If the rule is missing, create it manually

```powershell
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
```

Connect to the server via another computer

```powershell
ssh username@your-windows-ip-address
```

**Ubuntu**

```sh
sudo apt update && sudo apt install openssh-server
sudo systemctl enable --now ssh
```

If using a firewall like `ufw`

```sh
sudo ufw allow ssh
```

## Using Key-Based Authentication

**At the local (client) computer**

Generate a key pair,

```sh
ssh-keygen -t ed25519 -C "your_email@example.com"
```

The SSH agent will ask you to enter a location to save the keys like `/home/user/.ssh/id_ed25519`. The passphrase is optional.
Then there will be two SSH key files:

- `~/.ssh/id_ed25519` is the *private key*. **Protect it at all costs.**
- `~/.ssh/id_ed25519.pub` is the *public key*.

Create `~/.ssh/config`

```sh
mkdir -p ~/.ssh
chmod 700 ~/.ssh
touch ~/.ssh/config
chmod 600 ~/.ssh/config
```

Add the following content to set the *private key* as the `IdentityFile`.

```txt {filename="~/.ssh/config"}
Host *
    ServerAliveInterval 60    # Send a keep-alive packet every 60 seconds to prevent disconnection

# Define a host alias named "myserver"
Host myserver
    HostName 192.168.1.100           # The server's actual IP or domain name
    User your_username               # Login username
    Port 22                          # SSH port, defaults to 22 if not specified
    IdentityFile ~/.ssh/id_ed25519   # Path to the private key file used for this connection
```

And then you can use `ssh myserver` as a shorthand to connect the remote machine. You need to type in the password for the first login.

You can (and should) copy the public key over to the remote machine for a password-less login.

**Windows client**

```powershell
type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh user@your-server-ip "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys"
```

**Ubuntu client**

```sh
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@your-server-ip
```

### Harden your SSH server

Once you have established key-based (password-less) sudoer login. Consider disable login via a password to enhance security, especially when your PC is exposed to the internet. (directly or via port-forwarding)

Add a custom sshd config file

```sh
sudo nano /etc/ssh/sshd_config.d/10-custom.conf
```

with the content similar to this. [sshd config options](https://man7.org/linux/man-pages/man5/sshd_config.5.html).

```txt {filename="/etc/ssh/sshd_config.d/10-custom.conf"}
# /etc/ssh/sshd_config.d/10-custom.conf
# Custom sshd config by Wen-Wei Tseng (sosiristseng)
PasswordAuthentication no
PermitRootLogin no
# AllowUsers sosiristseng
X11Forwarding no
AllowAgentForwarding no
ClientAliveInterval 300
ClientAliveCountMax 2
```

After saving the file, test your configuration,

```sh
sudo sshd -t
```

Normally this should not print any output. If everything is right, restart the SSH service.

```sh
sudo systemctl restart ssh
```

### Key-based login for a new user

Adapted from [casper network docs](https://docs.casper.network/operators/setup/non-root-user).

1. Generate an SSH key pair in the user's computer

```sh
ssh-keygen -t ed25519 -C "newuser@myPC"
```

The new user should keep the private key in safety and give the admin the public key (`~/.ssh/id_ed25519.pub`).

2. Create the user on the server

Assuming the admin already logging in the server, create an account for the user.

```sh
sudo adduser <username>
```

3. Switch to that user and set up ssh access

```sh
sudo su - <username>
mkdir ~/.ssh
chmod 700 ~/.ssh
touch ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

4. Paste the content of the public key `id_ed25519.pub` into `.ssh/authorized_keys`.

```sh
echo "ssh-ed25519 AAAAC3Nza... newuser@myPC" | tee -a ~/.ssh/authorized_keys
```

5. Exit the current session, and verify the new connection.

```sh
ssh -i ~/.ssh/id_ed25519 <username>@server_ip
```

### Accessing GitHub repositories via SSH

Add `~/.ssh/config`

```sh
nano ~/.ssh/config
```

with the following content

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

## Transfer files over SSH

How to copy files through SSH

### tar

```sh
tar cvf - $localdir | ssh someone@somemachine '(cd destdir && tar xBf -)'
```

### rsync

Use a SSH remote as a source or a destination folder.

```sh
rsync -avh /source/folder/ username@serverip:/dest/folder/
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

## Port forwarding

**Local Port Forwarding**: You want to access a service on the remote server (or within its internal network) that is not directly reachable from the local machine, such as a database or internal web page.

```sh
ssh -L [local_address:]local_port:destination_host:destination_port user@ssh_server
```

For example,

```sh
ssh -N -L 8080:localhost:8888 user@remote-server.com
```

- `-L`: listen on local port 8080, and forward everything to port 8888 on the remote side. (accessing a service on the remote server)
- `-N`: not to execute a remote command and not to open an interactive shell. (this connection is used for port forwarding only)

Accessing `localhost:8080` on the local machine is now equivalent to accessing port `8888` on the remote server.

**Remote Port Forwarding**: The reverse of local port forwarding, exposing a local service to the remote.

```sh
ssh -R [remote_address:]remote_port:destination_host:destination_port user@ssh_server
```
