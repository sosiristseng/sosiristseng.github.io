---
title: Convert linear index to 2D indices
date: 2024-03-30
tags:
  - julia
---

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
