---
title: WSL2
tags:
- windows
- linux
---

Setup Windows subsystem for Linux 2 ([WSL2](https://docs.microsoft.com/en-us/windows/wsl/)) for Linux development experience in Windows 10 and 11.

## Instal WSL2

Open powershell with administrator privilege, [run the following command](https://devblogs.microsoft.com/commandline/install-wsl-with-a-single-command-now-available-in-windows-10-version-2004-and-higher/) in the host.

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

After reboot, run this command with admin privilege to install Ubuntu

```powershell
wsl --set-default-version 2
wsl --update
wsl --unregister Ubuntu  # Remove existing Ubuntu entry
wsl --install -d Ubuntu  # You can choose other distributions, e.g., Debian
wsl --manage Ubuntu --set-sparse true
```

## WSL2 post-install (optional) setup

### Move the virtual disk

If you want to move the WSL virtual disk file to another disk (in this example, `D:\`), run the following commands in Windows[^export-import][^movedrive]:

> [!tip]
> The following example will move the current WSL virtual disk to `D:\Ubuntu\ext4.vhdx`. You can change the distribution name (Ubuntu) and filesystem paths if necessary.

```powershell
cd D:\
mkdir WSL
cd WSL
mkdir Ubuntu

wsl --export Ubuntu .\Ubuntu\ext4.vhdx --vhd
wsl --unregister Ubuntu
wsl --import-in-place Ubuntu .\Ubuntu\ext4.vhdx
```

[^export-import]: https://learn.microsoft.com/zh-tw/windows/wsl/basic-commands#import-and-export-a-distribution
[^movedrive]: https://blog.iany.me/2020/06/move-wsl-to-another-drive/

### Default login user

Edit `/etc/wsl.conf` in the WSL. You may need to set the default user if you have moved the virtual disk file of the WSL distribution.

```txt title="/etc/wsl.conf"
[user]
default=username
```

### Host settings

Edit `.wslconfig` [^wslconfig] in your Windows home directory (Enter `%USERPROFILE%` in file explorer's location bar).

For example,

```txt title=".wslconfig"
[wsl2]
memory=20GB              # How much memory to assign to the WSL2 VM.
processors=4             # How many processors to assign to the WSL2 VM.
swap=8GB                 # How much swap space to add to the WSL2 VM. 0 for no swap file.
swapfile=C:\\temp\\wsl-swap.vhdx # Sets swapfile path location, default is %USERPROFILE%\AppData\Local\Temp\swap.vhdx. Useful if your C drive has limited disk space.
localhostForwarding=true # Boolean specifying if ports bound to wildcard or localhost in the WSL2 VM should be connectable from the host via localhost:port (default true).
```

[^wslconfig]: https://learn.microsoft.com/zh-tw/windows/wsl/wsl-config

### Auto reclaim RAM and disk space

Edit `.wslconfig` [^wslconfig] in your Windows home directory (Enter `%USERPROFILE%` in file explorer's location bar). [^autoreclaim]

```txt title=".wslconfig"
[experimental]
autoMemoryReclaim=dropcache
sparseVhd-true
```

[^autoreclaim]: https://devblogs.microsoft.com/commandline/windows-subsystem-for-linux-september-2023-update/

## Mantenance

### Update kernel

To (manually) update the WSL kernel, run the following commands with administrator privileges:

```powershell
wsl --shutdown
wsl --update
```

### Reclaim virtual disk space

To reclaim disk space from virtual hard disks (VHDs), run the following commands with administrator privileges [^optimize-vhd]:

```powershell
wsl --shutdown
Optimize-VHD -Path %path-to.vhdx% -Mode Full
```

[^optimize-vhd]: https://blog.miniasp.com/post/2023/05/14/Shrink-your-WSL2-Virtual-Disks-and-Docker-Images-and-Reclaim-Disk-Space



## Caveats about WSL2

### Poor filesystem performance across OSes

Cross-OS file access (e.g., accessing `/mnt/c` in WSL) is at least one order of magnitude slower than accessing the native (`/home/user/file`) files.[^wslio]

[^wslio]: https://neilbryan.ca/posts/win10-wsl2-performance/
