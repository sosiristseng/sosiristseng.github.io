---
title: Julia array tips
date: 2025-09-12
tags:
  - julia
---

## Convert vector of vector to matrix

Use the [stack](https://docs.julialang.org/en/v1/base/arrays/#Base.stack) function.

```julia
stack([[1,0,1],[0,0,1]], dims=1) == [ 1 0 1 ; 0 0 1 ]
```

## Convert linear index to 2D indices

Use `CartesianIndices((nrow, ncol))` [^1].

<!-- more -->

```julia
x = rand((7, 10))
CI = CartesianIndices((7, 10))
for i in 1:length(x)
    r = CI[i][1]
    c = CI[i][2]
    @assert x[i] == x[r, c]
end
```

[^1]: https://discourse.julialang.org/t/julia-usage-how-to-get-2d-indexes-from-1d-index-when-accessing-a-2d-array/61440
