---
title: Julia Tips
tags:
  - julia
---

Random tips about the Julia programming language.

+ [[julia-package-loading|Package Loading]] tips
+ [[julia-design-patterns| Design patterns and anitpatterns]]

## Visualization

+ [[plotsjl-tips|Plots.jl]] tips
+ [[pyplotjl-tips|PyPlot.jl]] tips

### Alternative to DisplayAs

In https://github.com/fredrikekre/Literate.jl, it is recommended to use https://github.com/tkf/DisplayAs.jl for notebook output to save the result size. If you don't want to add another dependency, you can use `display()` instead.

```julia
using Plots
PNG(img) = display("image/png", img)

plot(rand(6)) |> PNG
```

## Modeling and simulation

### Dealing with DomainErrors

`sqrt(x)`, `log(x)`, and `pow(x)` will throw `DomainError` exceptions with negative `x`, interrupting differential equation solvers. One can use these functions' counterparts in https://github.com/JuliaMath/NaNMath.jl, returning `NaN` instead of throwing a `DomainError`. Then, the solvers will reject the solution and retry with a smaller time step.

```julia
sqrt(-1.0) # throws DomainError

import NaNMath as nm
nm.sqrt(-1.0) # NaN
```

### Get the ODE Function (vector field) from an ODE system

`f = ODEFunction(sys)`

```julia
using ModelingToolkit
using DifferentialEquations
using Plots

# Independent (time) and dependent (state) variables (x and RHS)
@variables t x(t) RHS(t)

# Setting parameters in the modeling
@parameters τ

# Differential operator w.r.t. time
D = Differential(t)

# Equations in MTK use the tilde character (`~`) as equality.
# Every MTK system requires a name. The `@named` macro simply ensures that the symbolic name matches the name in the REPL.

@named fol_separate = ODESystem([
    RHS  ~ (1 - x)/τ,
    D(x) ~ RHS
])

sys = structural_simplify(fol_separate)

f = ODEFunction(sys)

f([0.0], [1.0], 0.0) # f(u, p, t) returns the value of D(x)
```

## Arrays

### How to get 2D indexes from a 1D index when accessing a 2D array?

`CartesianIndices(shape_in_tuple)`[^cartesian]

```julia
x = rand((7, 10))
CI = CartesianIndices((7, 10))
for i in 1:length(x)
    r = CI[i][1]
    c = CI[i][2]
    @assert x[i] == x[r, c]
end
```

[^cartesian]: https://discourse.julialang.org/t/julia-usage-how-to-get-2d-indexes-from-1d-index-when-accessing-a-2d-array/61440)
