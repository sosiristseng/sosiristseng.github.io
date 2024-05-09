---
title: robocopy
tags:
  - windows
  - command-line
---

[Robust copy (robocopy)](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/robocopy) is a file-copying command-line tool baked in Windows 10+.

## Usage

To see its commands

```powershell
robocopy /?
```

To mirror (`/MIR`) two folders with multithreading (`/MT`)

```powershell
robocopy SOURCE DESTINATION /MIR /MT
```
