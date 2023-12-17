---
title: Julia Tips
tags:
  - julia
---

Random tips about the Julia programming language.

+ [[julia-package-loading|Package Loading]] tips
+ [[julia-design-pattern| Design patterns and anitpatterns]]

## Visualization

+ [[plotsjl-tips|Plots.jl]] tips
+ [[pyplotjl-tips|PyPlot.jl]] tips

## Arrays

### How to get 2D indexes from a 1D index when accessing a 2D array?

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
