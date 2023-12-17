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

### Alternative to DisplayAs

In https://github.com/fredrikekre/Literate.jl, it is recommended to use https://github.com/tkf/DisplayAs.jl for notebook output to save result size. If you don't want to add another dipendency, you can use `display()` instead.

```julia
using Plots
PNG(img) = display("image/png", img)

plot(rand(6)) |> PNG
```

## Modeling and simulation

### Dealing with DomainErrors

`sqrt()` and `log()` will throw `DomainError` exceptions with negative float input, which could be problematic in differential equation solvers. One can use these functions in https://github.com/JuliaMath/NaNMath.jl, which return NaN instead of throwing a `DomainError`. Then the solver will reject the solution and retry with a smaller step.

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
