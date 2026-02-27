---
title: robocopy
tags:
  - command-line
  - windows
---

How to copy files with [robocopy](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/robocopy).

<!--more-->

To see its commands

```powershell
robocopy /?
```

For instance, to mirror (`/MIR`) two folders with multithreading (`/MT`)

```powershell
robocopy SOURCE DESTINATION /MIR /MT
```
