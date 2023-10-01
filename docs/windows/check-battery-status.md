---
title: Check battery status
tags:
  - windows
---

To check battery status and health, open Windows Powershell with Administrator rights and [run](https://www.pcmag.com/how-to/how-to-check-your-laptops-battery-health-in-windows-10)

```powershell
powercfg /batteryreport /output "C:\battery-report.html"
```

The report is `C:\battery-report.html`
