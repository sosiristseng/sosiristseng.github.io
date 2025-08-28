---
title: Convert vector of vector to matrix
date: 2024-10-07
tags:
  - julia
---

Use the [stack](https://docs.julialang.org/en/v1/base/arrays/#Base.stack) function.

```julia
stack([[1,0,1],[0,0,1]], dims=1) == [ 1 0 1 ; 0 0 1 ]
```
