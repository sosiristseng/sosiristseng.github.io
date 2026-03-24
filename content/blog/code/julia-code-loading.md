---
title: Julia code loading
date: 2026-02-28
tags:
- julia
---

The documentation about Julia code loading: https://docs.julialang.org/en/v1/manual/code-loading/

See also [Julia package management](julia-pkg-management.md)

<!--more-->

## Include other files as submodules

You could include julia files as submodules like this

```julia {filename="main.jl"}
## main.jl
include("foo.jl")
using .Foo

include("bar.jl")
using .Bar
```

```julia {filename="foo.jl"}
## foo.jl
module Foo
# content of Foo module
end
```

```julia {filename="bar.jl"}
## bar.jl
module Bar
# content of Bar module
end
```

- Best when the submodules are used exclusively for this project and will not be shared with others.
- Usually you want to include all dependent submodules in the top-most file, [like a table of contents](https://discourse.julialang.org/t/ann-patmodules-jl-a-better-module-system-for-julia/52226/40).
- The `include` and `using` lines need to be re-execute when the code in the submodule changes. (if `Revise.includet("foo.jl")` is not used)
- Use [relative module path](https://stackoverflow.com/questions/54410557/submodule-intra-dependencies-in-julia) when `Bar` depends on `Foo`.

### FromFile.jl

[FromFile.jl](https://github.com/Roger-luo/FromFile.jl) provides a macro `@from` to replace `include()`. Using `@from` to access a file multiple times (for example calling `@from` "file.jl" import foo in multiple files) will access the same objects each time; i.e. without the duplication issues that `include("file.jl")` would introduce.

```julia {filename="file1.jl"}
# file1.jl
import FromFile: @from
@from "file2.jl" import foo

bar() = foo()
```
```julia {filename="file2.jl"}
#file2.jl
foo() = println("hi")
```

## Code loading in a Package

To create a minimal package in the REPL (package mode)

```
pkg> generate JuliaHello
```

In this example, `main.jl` has access to the `JuliaHello` module, because Julia sees `src/JuliaHello.jl` as an entry point for the `JuliaHello` package / module.

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
