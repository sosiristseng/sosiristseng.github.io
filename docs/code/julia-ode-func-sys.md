---
title: Get the ODE Function from an ODE system
date: 2024-03-31
tags:
  - julia
  - ode
---

`f = ODEFunction(sys)` could be useful in plotting vector fields.

<!-- more -->

```julia
using ModelingToolkit
using DifferentialEquations

# Independent (time) and dependent (state) variables (x and RHS)
@independent_variables t
@variables x(t) RHS(t)

# Setting parameters in the modeling
@parameters τ

# Differential operator w.r.t. time
D = Differential(t)

# Equations in MTK use the tilde character (`~`) as equality.
# Every MTK system requires a name. The `@named` macro simply ensures that the symbolic name matches the name in the REPL.

@mtkbuild sys = ODESystem([
    RHS  ~ (1 - x)/τ,
    D(x) ~ RHS
])

tend = 2.0
prob = ODEProblem(sys, [x=>0.0], tend, [τ=>1.0])

prob.f([0.0], prob.p, 0.0) # f(u, p, t) returns the value of D(x)
```
