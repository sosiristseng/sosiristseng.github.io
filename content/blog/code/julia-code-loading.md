---
title: Julia code loading
date: 2026-02-28
tags:
- julia
---

The documentation about Julia code loading: https://docs.julialang.org/en/v1/manual/code-loading/

See also [Julia package management](julia-pkg-management.md)

<!--more-->

## Package loading

`main.jl` has access to the `JuliaHello` module because Julia sees `src/JuliaHello.jl` as an entry point for the `JuliaHello` package / module.

```julia {filename="src/JuliaHello.jl"}
## src/JuliaHello.jl
module JuliaHello
greet() = print("Hello World!")
end # module
```

```julia {filename="main.jl"}
## main.jl
using JuliaHello
JuliaHello.greet()
```

## "Developing" a temporary package

Use the Julia Pkg command `dev --local pkg...`

[Julia docs | Pkg | dev](https://docs.julialang.org/en/v1/stdlib/Pkg/)

Assuming we have the file structure for the packages

```
. present working directory (pwd)
| - main.jl
| - Manifest.toml
| - Project.toml
|
+---Mod1.jl
|   | - Manifest.toml (optional)
|   | - Project.toml
|   |
|   \---src
|         - Mod1.jl
|
\---Mod2.jl
    | - Manifest.toml (optional)
    | - Project.toml
    |
    \---src
          - Mod2.jl
```

Add local packages and track the file changes in the Julia REPL

```julia
julia> ]
pkg> activate .
pkg> dev --local Mod1 Mod2
```

Or run the commands in the Julia script

```julia
import Pkg

# To generate Project.toml if not present
Pkg.activate(".")

Pkg.develop(PackageSpec(path="Mod1.jl"))
Pkg.develop(PackageSpec(path="Mod2.jl"))
```

- Best when `Mod1` and `Mod2` are modified frequently and shared.
- Loaded code is determined by local files instead of package versions.
- The updates are loaded when `using` is invoked, along with precompilation. [Revise.jl](https://timholy.github.io/Revise.jl/stable/) tracks and updates modified files and you don't have to restart the Julia process upon module code changes.
