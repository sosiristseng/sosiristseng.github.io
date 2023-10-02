---
title: WSL2
tags:
- windows
- linux
---

Setup Windows subsystem for Linux 2 ([WSL2](https://docs.microsoft.com/en-us/windows/wsl/)) for Linux developement experience in Windows 10 and 11.

## Instal WSL2

Open powershell with administrator privilege, [run the following command](https://devblogs.microsoft.com/commandline/install-wsl-with-a-single-command-now-available-in-windows-10-version-2004-and-higher/) in the host.

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

After reboot, run this command wiht admin privilege to install Ubuntu

```powershell
wsl --set-default-version 2
wsl --install -d Ubuntu  # You can choose other distributions e.g. Debian
```

## WSL2 post-install setup

### Enable systemd

Edit `/etc/wsl.conf` in the WSL OS.

```txt title="/etc/wsl.conf"
[boot]
systemd=true
```

### Default login user (optional)

Edit `/etc/wsl.conf` in the WSL OS.

```txt title="/etc/wsl.conf"
[user]
default=username
```

### Move virtual disk (optional)

If you want to move the WSL virtual disk file to another disk (in this example, `D:\`), run this script in the host[^export-import][^movedrive]:

> [!tip]
> The following example usse `D:\Ubuntu\ext4.vhdx` as the virtual disk. You can change the distribution name (Ubuntu) and filesystem paths as needed.

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

## Mantenance

### Update WSL kernel

To (manually) update WSL kernel, run this script in Powershell with administrator privileges:

```powershell
wsl --shutdown
wsl --update
```

### Reclaim virtual disk space

To reclaim disk space from virtual harddisks (VHDs), run this script in Powershell with administrator privileges[^optimize-vhd]:

```powershell
wsl --shutdown
Optimize-VHD -Path <path-to.vhdx> -Mode Full
```

[^optimize-vhd]: https://blog.miniasp.com/post/2023/05/14/Shrink-your-WSL2-Virtual-Disks-and-Docker-Images-and-Reclaim-Disk-Space

## Host settings

Edit `.wslconfig`.[^wslconfig] in your Windows home directory (Enter `%USERPROFILE%` in file explorer's location bar).

For example,

```sh title=".wslconfig"
[wsl2]
memory=20GB              # How much memory to assign to the WSL2 VM.
processors=4             # How many processors to assign to the WSL2 VM.
swap=8GB                 # How much swap space to add to the WSL2 VM. 0 for no swap file.
swapfile=C:\\temp\\wsl-swap.vhdx # Sets swapfile path location, default is %USERPROFILE%\AppData\Local\Temp\swap.vhdx. Useful if your C drive has limited disk space.
localhostForwarding=true # Boolean specifying if ports bound to wildcard or localhost in the WSL2 VM should be connectable from the host via localhost:port (default true).
```

[^wslconfig]: https://learn.microsoft.com/zh-tw/windows/wsl/wsl-config

## Caveats about WSL2

### Poor filesystem performance across OS

Cross-OS file access (E.G., git accessing repositories in  `/mnt/c`) is at least one order of magnitude slower than native one.[^wslio]

[^wslio]: https://neilbryan.ca/posts/win10-wsl2-performance/

### 1GB RAM cost for the hypervisor

As [this reddit post](https://www.reddit.com/r/bashonubuntuonwindows/comments/wo6729/the_hidden_costs_of_wsl2_memory_usage/) and the [Hyper-V documentation](https://learn.microsoft.com/en-us/windows-server/administration/performance-tuning/role/hyper-v-server/memory-performance) said, running Windows and WSL side-by-side on a hypervisor takes 1GB of RAM.
