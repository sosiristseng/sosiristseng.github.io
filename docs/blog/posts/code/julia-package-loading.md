---
title: Julia package loading
date: 2025-02-19
tags:
  - julia
---

When your Julia codebase grows larger, you might want to organize it into modules and packages.

## Include other files as submodules

You could include jl files as submodules like this

```julia title="main.jl"
include("foo.jl")
using .Foo

include("bar.jl")
using .Bar
```

```julia title="foo.jl"
module Foo
# content of Foo module
end
```

```julia title="bar.jl"
module Bar
# content of Bar module
end
```

- Best when the submodules are used exclusively for this project and will not be shared with others.
- Usually you want to include all dependent submodules in the top-most file, [like a table of contents](https://discourse.julialang.org/t/ann-patmodules-jl-a-better-module-system-for-julia/52226/40).
- The `include` and `using` lines need to be re-execute when the code in the submodule changes. (if `Revise.includet("foo.jl")` is not used)
- Use [relative module path](https://stackoverflow.com/questions/54410557/submodule-intra-dependencies-in-julia) when `Bar` depends on `Foo`.
- There may be recursive `include()` calls and `replace module` warnings. [FromFile.jl](https://github.com/Roger-luo/FromFile.jl) can deal with these file inclusion duplications.

## Automatic package loading in a project

In this example, the project folder is `JuliaHello`. Note that `main.jl` has access to the `JuliaHello` module automatically.

![image](https://user-images.githubusercontent.com/40054455/134101300-ce73796d-e5b5-4687-a0be-c083f8d146f1.png)


```julia title="src/JuliaHello.jl"
module JuliaHello
greet() = print("Hello World!")
end # module
```

```julia title="main.jl"
using JuliaHello
JuliaHello.greet()
```

## "Developing" a temporary package

Us the Julia Pkg command `dev --local pkg...`

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

```julia-repl
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

## Make a hosted package

Make a Git repo for your custom package and publish it to Git service providers, e.g. GitHub / Gitlab. And then you can `]add https://github.com/username/Mod1.jl.git`

[PkgTemplates.jl](https://github.com/invenia/PkgTemplates.jl) or [PkgSkeleton.jl](https://github.com/tpapp/PkgSkeleton.jl) is recommended to generate package with unit tests and CI/CD settings.

Nonetheless, it's just one step away from proper [registeration](https://github.com/JuliaRegistries/Registrator.jl) to the general Julia registry to be used by more people.

### Unit testing

You can have [local dependencies](https://julialang.github.io/Pkg.jl/v1/creating-packages/#Test-specific-dependencies-in-Julia-1.2-and-above) for running tests in `test/Project.toml` without the need of `extra` and `targets` sections in the main project's `Project.toml`.

Though the build-in [unit-test framework](https://docs.julialang.org/en/v1/stdlib/Test/) is good, but [Jive.jl](https://github.com/wookay/Jive.jl) provides more flexibilities. See [TestJive.jl](https://github.com/wookay/TestJive.jl) for code examples.

- Discover unit testing `jl` files automatically.
- Skip or select which test(s) to run.
- Multiprocessing for faster runs.

### Documentation

Use [Documenter.jl](https://juliadocs.github.io/Documenter.jl/stable/) to generate the documentation for Julia packages.

You need [an SSH deploy key](https://juliadocs.github.io/Documenter.jl/stable/lib/public/#DocumenterTools.genkeys) to deploy docs to GitHub pages.

```julia
using DocumenterTools
DocumenterTools.genkeys(user="you", repo="YourPackage.jl")
```

### Continuous integration / delivery (CI/CD)

`PkgTemplates.jl` should set up the appropriate code structure for you. I would recommend to use GitHub to host Julia packages because

- Running GH actions is unlimited for public repositories, with multiple operating systems running concurrently (matrix build).
- Julia github actions are convenient to use.
- Automation bots integrate better with GitHub. e.g. TagBot, Registerbot, and Compat Helper.

## Reference

- [Julia workflow tips](https://docs.julialang.org/en/v1/manual/workflow-tips/)
- [Pkg.jl docs](https://julialang.github.io/Pkg.jl/v1/)
- [Comparison between v0.6 and v0.7 (SO)](https://stackoverflow.com/questions/36398629/change-package-directory-in-julia/36400065#36400065)
- [Developing your Julia package (Medium post)](https://medium.com/coffee-in-a-klein-bottle/developing-your-julia-package-682c1d309507)
- [YouTube: Developing Julia packages by Chris](https://youtu.be/QVmU29rCjaA)
