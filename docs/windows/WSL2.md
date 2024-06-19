---
title: WSL2
tags:
- windows
- linux
---

Set up Windows subsystem for Linux 2 ([WSL2](https://docs.microsoft.com/en-us/windows/wsl/)) for Linux development experience in Windows 10 and 11.

## Instal WSL2

Open powershell with administrator privilege, [run the following command](https://devblogs.microsoft.com/commandline/install-wsl-with-a-single-command-now-available-in-windows-10-version-2004-and-higher/) in the host.

```powershell
wsl --install
```

or install the components [manually](https://learn.microsoft.com/en-us/windows/wsl/install-manual)

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

After reboot,

```powershell
wsl --update
wsl --set-default-version 2
wsl --install -d Ubuntu  # Or another distro
```

## WSL2 post-install (optional) setup

### Backup/move the virtual disk

If you want to move the WSL virtual disk file to another disk (in this example, `D:\`), run the following commands in Windows[^export-import][^movedrive]:

```powershell
wsl --export Ubuntu .\Ubuntu\ext4.tar
wsl --unregister Ubuntu
wsl --import Ubuntu D:\Ubuntu\ .\Ubuntu\ext4.tar
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
swapfile=C:\\temp\\wsl-swap.vhdx # Sets swap file path location, default is %USERPROFILE%\AppData\Local\Temp\swap.vhdx. Useful if your C drive has limited disk space.
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

## Maintenance

### Update kernel

To (manually) update the WSL kernel, run the following commands with administrator privileges:

```powershell
wsl --shutdown
wsl --update
```

### Reclaim virtual disk space

#### Optimize-VHD
To reclaim disk space from virtual hard disks (VHDs), run the following commands with administrator privileges [^optimize-vhd]:

```powershell
wsl --shutdown
Optimize-VHD -Path %path-to.vhdx% -Mode Full
```

#### diskpart
Alternatively, use `diskpart` (if `Optimize-VHD` is not found) [^vhd-diskpart]

```powershell
wsl --shutdown
diskpart
# open window Diskpart
select vdisk file="E:\ubuntu\ext4.vhdx"
attach vdisk readonly
compact vdisk
detach vdisk
exit
```

#### Export and re-import

Alternatively, export the VHD as a tar file and reimport it again.

[^optimize-vhd]: https://blog.miniasp.com/post/2023/05/14/Shrink-your-WSL2-Virtual-Disks-and-Docker-Images-and-Reclaim-Disk-Space
[^vhd-diskpart]: https://answers.microsoft.com/en-us/windows/forum/all/optimize-vhd-not-found-in-windows-10-home/a727b760-0f82-4d0f-8480-d49eeaeb11a2

## Caveats about WSL2

### Poor filesystem performance across OSes

Cross-OS file access (e.g., accessing `/mnt/c` in WSL) is at least one order of magnitude (10x) slower than accessing natively (`/home/user/`).[^wslio]

[^wslio]: https://neilbryan.ca/posts/win10-wsl2-performance/
