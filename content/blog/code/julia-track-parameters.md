---
title: Track parameter changes in simulations
date: 2025-02-19
tags:
- julia
---

From this [discourse thread](https://discourse.julialang.org/t/save-and-plot-parameter-history-with-modelingtoolkit-jl/81778)

<!--more-->

Changing parameters using traditional `DiffEqCallbacks.jl` with `prob.ps[sym] = val` in the middle of a simulation cannot be tracked.

From v10, `ModelingToolkit.SymbolicDiscreteCallback` can track changed parameters in a callback. See https://docs.sciml.ai/ModelingToolkit/dev/basics/Events/#save_discretes

For example,

```julia
ev = ModelingToolkit.SymbolicDiscreteCallback(
    [1.0] => [iStim ~ 5],
    discrete_parameters = iStim,
    iv = t)
@mtkcompile sys = ODESystem([D(x) ~ rhs, rhs ~ -x + v_istim, v_istim ~ iStim], t; discrete_events = [ev])
prob = ODEProblem(sys, [], (0, 10.0))
@time sol = solve(prob)
```
