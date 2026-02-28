---
title: Julia design patterns
date: 2025-02-19
tags:
- julia
---

Some notes of Tom Kwong's book [Hands on Design patterns in Julia](https://www.packtpub.com/product/hands-on-design-patterns-and-best-practices-with-julia/9781838648817).

<!--more-->

## Separated Project environments

It is recommended to maintain a minimal root environment (with a few necessary packages like `Revise.jl`) and [customize the local Julia project environment](https://opensourc.es/blog/all-about-pkg/#environments) by the following steps:

1. Go to your project folder and run `julia --project=.`. This will run `pkg> activate .` at start.
2. Add you packages by `pkg> add Pkg1 Pkg2...`

## Packages and modules

Julia also encourages making your own packages, even temporarily, to utilize unit-testing, precompilation, and to separate namespaces.

- Creating Julia packages is light-weight: `pkg> generate PkgName` only creates two files (one julia and one TOML file). For a more complete configuration, consider using [PkgTemplates](https://github.com/invenia/PkgTemplates.jl) or [PkgSkeleton.jl](https://github.com/tpapp/PkgSkeleton.jl) for more functionalities like CI testing and code coverage.
- [Revise.jl](https://github.com/timholy/Revise.jl) watches file system changes and update the code in the loaded packages / modules automatically.

## Functional interfaces and multiple dispatch

In the Julia world, generic functions called [functions](https://docs.julialang.org/en/v1/manual/functions/), while those with type annotations / parameterizations are called [methods](https://docs.julialang.org/en/v1/manual/methods/). My impressions so far was that, Julia is a _functional interface-first_ programming language, by the power of [multiple dispatch paradigm](https://opensourc.es/blog/basics-multiple-dispatch/), to make Julia a much more flexible (in programming) and composable between packages: e.g. [DiffEq + Flux + GPU kernel](https://github.com/SciML/DiffEqFlux.jl), and mathematically natural. However, it requires a vastly different mindset for users coming from the object-oriented worlds like Python / Java.

- Abstract types cannot have fields. They are only meant to be inherited with their functional interfaces. Concrete types (structs with fields), on the other hand, cannot not be inherited.
- Use parametric [type (structs)](https://docs.julialang.org/en/v1/manual/types/#Parametric-Types) and [methods](https://docs.julialang.org/en/v1/manual/methods/#Parametric-Methods) rather than directly type-annotate the fields / arguments.
- Traits are functions that return True/False/Error based on the input type.

## Delegation pattern

This is a form of polymorphism via composition[^1]. Use a new wrapper type to established packages to reuse their code at the cost of an additional layer of indirection.

[^1]: https://stackoverflow.com/questions/54789937/what-is-delegation-in-julia

## Holy traits

[Holy traits](https://invenia.github.io/blog/2019/11/06/julialang-features-part-2/) are named after Tim Holy.

- Traits are empty structs.
- Data types are assigned categorically to traits' interfaces, implementing different behavior for different kind of data type.
- Traits hierarchy could be separated from the type hierarchy they modeled.

[SimpleTraits.jl](https://github.com/mauro3/SimpleTraits.jl) automates some of the boilerplate for you.

## Global constants

Global (module-level) variables are discouraged for performance reasons, but global constants are welcomed in Julia since the compiler can optimize global constants.

## Struct of arrays (SoA)

Struct of arrays (SoA) is faster than to array of structs (AoS) because of being cache-friendly.

[StructArrays](https://github.com/JuliaArrays/StructArrays.jl) handles the mapping of AoS (on the interface) to SoA (in the memory).

## Memoization

Memoization saves duplicated work in repetitive or recursive calls.

[Memoize.jl](https://github.com/JuliaCollections/Memoize.jl) can do function wrapper, local cache, and closures for you.

## Barrier functions for type stability

Julia runs slower in type-unstable code. Use `@code_warntype` in front of an expression to spot type instability. (or use `@inferred` in unit tests to err on type instabilities) Use generic functions (aka barrier functions) to ensure type stability.

e.g.
- `zero(x)` instead of `0`.
- [Separate kernel functions](https://docs.julialang.org/en/v1/manual/performance-tips/#kernel-functions). Small functions are more easily optimized.

## Keyword definition

Keyword definitions use less boilerplate code for struct initialization.

- [Parameters.jl](https://github.com/mauro3/Parameters.jl) package.
- Built-in `Base.@kwdef`.

## Accessor: getters and setters

Customize `Base.getproperty(x, :a)` for getters (`x.a`) and `Base.setproperty!(x, :a, val)` for setters (`x.a = val`).

## Let blocks

A `let` block defines its own local namespace. The variables defined inside a let block cannot be accessed outside.

## Functional pipes

Useful in data pipelines. Checkout [Chain.jl](https://github.com/jkrumbiegel/Chain.jl) for enhanced pipelines.

## Anti-patterns in Julia

1. *Type instability* especially in tight loops yields poor performance.
2. *Global variables* are type-unstable. But *Global constants* are not.
3. Type piracy, a.k.a. redefining an existing function or twisting the behavior of a function. *Do not define methods for types you do not own*.
4. Narrow argument types means overspecialization. Write generic code first.
5. Non-concrete field type: `struct A x::Real end` provides no benefit against `struct A x end`. Use parametric types like the example below, or use [ConcreteStructs.jl](https://github.com/jonniedie/ConcreteStructs.jl).

```julia
struct A{T<:Real}
  x::T
end
```

## References

- [Julia docs](https://docs.julialang.org/en/v1/)
- [opensourc.es](https://opensourc.es/)
- [Hands on Design patterns in Julia](https://www.packtpub.com/product/hands-on-design-patterns-and-best-practices-with-julia/9781838648817)
