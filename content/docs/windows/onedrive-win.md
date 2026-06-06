---
title: OneDrive (Windows)
tags:
  - windows
---

## Fix OneDrive link not working in the Explorer sidebar

You can try to unlink your OneDrive account and relink it back, or:

apply the following registry to fix OneDrive in the Explorer. [^fix-onedrive] You might need to change the `RelativePath` entry.

```txt {filename="fix-onedrive.reg"}
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{A52BBA46-E9E1-435f-B3D9-28DAA648C0F6}]
"Attributes"=dword:00000001
"Category"=dword:00000004
"DefinitionFlags"=dword:00000040
"Icon"=hex(2):25,00,53,00,79,00,73,00,74,00,65,00,6d,00,52,00,6f,00,6f,00,74,\
  00,25,00,5c,00,73,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,00,5c,00,69,00,\
  6d,00,61,00,67,00,65,00,72,00,65,00,73,00,2e,00,64,00,6c,00,6c,00,2c,00,2d,\
  00,31,00,30,00,34,00,30,00,00,00
"LocalizedName"=hex(2):40,00,25,00,53,00,79,00,73,00,74,00,65,00,6d,00,52,00,\
  6f,00,6f,00,74,00,25,00,5c,00,53,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,\
  00,5c,00,53,00,65,00,74,00,74,00,69,00,6e,00,67,00,53,00,79,00,6e,00,63,00,\
  43,00,6f,00,72,00,65,00,2e,00,64,00,6c,00,6c,00,2c,00,2d,00,31,00,30,00,32,\
  00,34,00,00,00
"LocalRedirectOnly"=dword:00000001
"Name"="OneDrive"
"ParentFolder"="{5E6C858F-0E22-4760-9AFE-EA3317B67173}"
"ParsingName"="shell:::{018D5C66-4533-4307-9B53-224DE2ED1FE6}"
"RelativePath"="OneDrive"

[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{A52BBA46-E9E1-435f-B3D9-28DAA648C0F6}]
"Attributes"=dword:00000001
"Category"=dword:00000004
"DefinitionFlags"=dword:00000040
"Icon"=hex(2):25,00,53,00,79,00,73,00,74,00,65,00,6d,00,52,00,6f,00,6f,00,74,\
  00,25,00,5c,00,73,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,00,5c,00,69,00,\
  00,31,00,30,00,34,00,30,00,00,00
"LocalizedName"=hex(2):40,00,25,00,53,00,79,00,73,00,74,00,65,00,6d,00,52,00,\
  6f,00,6f,00,74,00,25,00,5c,00,53,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,\
  00,5c,00,53,00,65,00,74,00,74,00,69,00,6e,00,67,00,53,00,79,00,6e,00,63,00,\
  43,00,6f,00,72,00,65,00,2e,00,64,00,6c,00,6c,00,2c,00,2d,00,31,00,30,00,32,\
  00,34,00,00,00
"LocalRedirectOnly"=dword:00000001
"Name"="OneDrive"
"ParentFolder"="{5E6C858F-0E22-4760-9AFE-EA3317B67173}"
"ParsingName"="shell:::{018D5C66-4533-4307-9B53-224DE2ED1FE6}"
"RelativePath"="OneDrive"
```

[^fix-onedrive]: https://ibug.io/blog/2025/04/windows-10-ltsc-onedrive-explorer-sidebar-fix/
