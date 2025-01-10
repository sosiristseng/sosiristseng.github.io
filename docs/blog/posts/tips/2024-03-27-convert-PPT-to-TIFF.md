---
title: Convert powerpoint slides to TIFF images
date: 2024-03-27
tags:
  - windows
  - powerpoint
  - research
  - tiff
categories:
  - Tips
---

How to export high resolution TIFF images from PowerPoint slides.

<!-- more -->

## Advanced save options

File -> Save a copy -> More options -> Save as type: TIFF -> Tools -> compress pictures -> choose the DPI you want -> save.

## Change default export settings

The export resolution is 96 dpi by default. You can edit the Windows registry to change it.

Save the following content as `dpi-300.reg`. Then, double click the `dpi-300.reg` to change the default exporting dpi to 300.

```txt title="dpi-300.reg"
Windows Registry Editor Version 5.00
[HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\PowerPoint\Options]
"ExportBitmapResolution"=dword:0000012C
```

> [!NOTE]
>  For older MS office suite, please see the [original article](https://learn.microsoft.com/en-us/office/troubleshoot/powerpoint/change-export-slide-resolution) for the corresponding version number.
