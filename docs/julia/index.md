---
title: Julia Tips

tags:
  - julia
---
Tips about Julia the programming language.

## Setup Julia

[[setup-julia|Set up Julia]]
## How to get 2D indexes from a 1D index when accessing a 2D array?


Use `CartesianIndices`. [Source](https://discourse.julialang.org/t/julia-usage-how-to-get-2d-indexes-from-1d-index-when-accessing-a-2d-array/61440)

```julia
x = rand((7, 10))
CI = CartesianIndices((7, 10))
for i in 1:length(x)
    r = CI[i][1]
    c = CI[i][2]
    @assert x[i] == x[r, c]
end
```
