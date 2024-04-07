---
title: Get the ODE Function from an ODE system
date: 2024-03-31
tags:
  - julia
---

`f = ODEFunction(sys)` could be useful in plotting vector fields.

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
