---
title: No more DomainErrors in Julia
date: 2024-04-02
tags:
  - julia
---

Use https://github.com/JuliaMath/NaNMath.jl.

<!-- more -->

`sqrt(x)`, `log(x)`, and `pow(x)` will throw `DomainError` exceptions with negative `x`, interrupting differential equation solvers. One can use these functions' counterparts in https://github.com/JuliaMath/NaNMath.jl, returning `NaN` instead of throwing a `DomainError`. Then, the solvers will reject the solution and retry with a smaller time step.

```julia
sqrt(-1.0) # throws DomainError

import NaNMath as nm
nm.sqrt(-1.0) # NaN
```
