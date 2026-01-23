---
title: onedrive (Linux)
tags:
  - linux
---

The linux OneDrive client https://github.com/abraunegg/onedrive seamlessly supports OneDrive Personal, OneDrive for Business, OneDrive for Office365, and SharePoint Libraries. **See also** the GUI for the OneDrive client: https://github.com/bpozdena/OneDriveGUI.

## Setup

### Install (Ubuntu)

Follow the [instructions](https://github.com/abraunegg/onedrive/blob/master/docs/ubuntu-package-install.md):

```sh
wget -qO - https://download.opensuse.org/repositories/home:/npreining:/debian-ubuntu-onedrive/xUbuntu_24.04/Release.key | gpg --dearmor | sudo tee /usr/share/keyrings/obs-onedrive.gpg > /dev/null
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/obs-onedrive.gpg] https://download.opensuse.org/repositories/home:/npreining:/debian-ubuntu-onedrive/xUbuntu_24.04/ ./" | sudo tee /etc/apt/sources.list.d/onedrive.list
sudo apt update && sudo apt install --no-install-recommends --no-install-suggests onedrive
```

### Authorize the Application

[Run](https://github.com/abraunegg/onedrive/blob/master/docs/usage.md#authorise-the-application-with-your-microsoft-onedrive-account) `onedrive` and visit the listed links.

```sh
onedrive
```

### Show config

```sh
onedrive --display-config
```

### Check if onedrive runs

```sh
onedrive --sync --dry-run
```

The default folder for OneDrive files is `~/OneDrive`.

If everything is OK, then download the OneDrive files

```sh
onedrive --sync --verbose
```

### Set maximal number of watched files

The `onedrive` client will watch a lot of files for synchronization and they may exceed the system limit (e.g., 65536). You can check the limits via:

```sh
sysctl fs.file-max
```

for the maximal number of files. And

```sh
sysctl fs.inotify.max_user_watches
```

for the maximal number of file watches.

You can increase the value by editing `/etc/sysctl.conf`

```txt title="/etc/sysctl.conf"
fs.inotify.max_user_watches=1048576
```

### Run onedrive client as a service

```sh
systemctl --user enable onedrive
systemctl --user start onedrive
```

To check the service's status:

```sh
systemctl --user status onedrive.service
```

To view the systemd application logs:

```sh
journalctl --user-unit=onedrive -f
```

The `onedrive` client will run in the monitor mode (`onedrive --monitor`), checking the file changes from local and remote and update them periodically.
