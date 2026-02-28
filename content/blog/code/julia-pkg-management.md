---
title: Package management in Julia
date: 2026-02-28
tags:
- julia
---

Official documentation for `Pkg.jl`: https://pkgdocs.julialang.org/

<!--more-->

## Show which package(s) could be updated

```julia
using Pkg
Pkg.status(; outdated=true)
```

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

## Make a Julia package

To create a minimal package:

```
pkg> generate HelloWorld
```

But it's recommended to use [PkgTemplates.jl](https://github.com/JuliaCI/PkgTemplates.jl) for the CI, unit tests, documentation, etc.

You could also [register your package](https://github.com/JuliaRegistries/Registrator.jl) to the general Julia registry to be accessible to Julia users.

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
