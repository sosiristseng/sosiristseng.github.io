---
title: IJulia use Python package provided by CondaPkg
date: 2024-10-07
tags:
  - julia
  - jupyter
categories:
  - code
---

[Source: stackoverflow](https://stackoverflow.com/questions/78130757/how-to-run-ijulia-using-the-pythoncall-condapkg-python-installation-rather-than)

Set the `JUPYTER` environment variable to `CondaPkg.jl`-provided `jupyter` and `IJulia.jl` will take it to start the kernel.

```julia
using CondaPkg
CondaPkg.add("jupyter")
ENV["JUPYTER"] = CondaPkg.which("jupyter")

using Pkg
Pkg.add("IJulia") # if IJulia was not yet installed
Pkg.build("IJulia") # To change the configuration of existing installation
```
