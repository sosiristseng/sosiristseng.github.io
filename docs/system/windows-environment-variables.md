---
title: Windows environment variables
tags:
  - windows
---

[Environment variables in Powershell](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_environment_variables?view=powershell-7.3)

## Session variables

Variables created by `set` are bound to the current session and not persistent.

```powershell
$Env:FOO = "example"
$Env:FOO
```

## Persistent variables

+ GUI: Windows Settings -> Advanced system settings -> Set **Environment Variables**.
+ Powershell: `[Environment]::SetEnvironmentVariable('KEY', 'VAL', 'Machine')`
+ Cmd: `SETX KEY VAL`
