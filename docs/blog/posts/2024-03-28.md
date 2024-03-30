---
title: Check battery status
date: 2024-03-28
tags:
- windows
---

Open Windows Powershell with Administrator rights and [run](https://www.pcmag.com/how-to/how-to-check-your-laptops-battery-health-in-windows-10):

```powershell
powercfg /batteryreport /output "C:\battery-report.html"
```

The report is at `C:\battery-report.html`.
