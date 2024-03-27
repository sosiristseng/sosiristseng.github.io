---
title: GPU driver timeout fix
tags:
  - windows
  - gpu
---

Some methods to fix GPU driver timeout/freeze.

## Upgrade BIOS firmware if you can

Check the product support page and upgrade to the latest BIOS version. (My PN53 mini PC was saved by a BIOS upgrade)

## Upgrade / Downgrade GPU drivers

For more stability, boot Windows in [safe mode](https://support.microsoft.com/en-us/windows/start-your-pc-in-safe-mode-in-windows-10-92c27cff-db89-8644-1ce4-b3e5e56fe234) and run [display driver uninstaller](https://www.guru3d.com/files-details/display-driver-uninstaller-download.html) (DDU) to remove the existing GPU driver.

### NVidia Minimal GPU driver

You can [nvcleaninstall](https://www.techpowerup.com/download/techpowerup-nvcleanstall/) to install Nvidia driver without bloat.

## Disable Multi-Plane Overlay (MPO)

Multi-Plane Overlay (MPO) may cause driver issues. You can disable MPO using the registry editor.

Save the following content as `disable-mpo.reg`. Then, double click the `disable-mpo.reg` to apply the registry.

```txt title="disable-mpo.reg"
Windows Registry Editor Version 5.00
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Dwm]
"OverlayTestMode"=dword:00000005
```
