---
title: Setup Julia
tags:
  - julia
  - linux
  - windows
---

## Install Julia

Install Julia with the [juliaup](https://github.com/JuliaLang/juliaup) installer.

### Linux/MacOS

```sh
curl -fsSL https://install.julialang.org | sh -s -- -y
```

### Windows

```powershell
winget install julia -s msstore
```

Alternatively, download and install [Julia official binaries](https://julialang.org/downloads/).

```powershell
winget install JuliaLang.Julia
```

## Post-install configurations

### Auto-activate local projects

Set environment variable `JULIA_PROJECT=@.` to let Julia automatically load the closest upstream `Project.toml` and activate the environment.

```sh title="~/.profile"
export JULIA_PROJECT=@.
```


!!! info

    `IJulia.jl`, the Julia kernel for Jupyter notebooks, sets `JULIA_PROJECT=@.` by default. Thus, Jupyter notebooks load their local Julia environments automatically.

!!! warning

    Loading local environments unconditionally is unsafe in untrusted sources, as shown in [Nefarious.jl](https://github.com/StefanKarpinski/Nefarious.jl). That is why Julia doesn't run `julia --project=@.` by default.

### Fully utilize CPU threads

Set environment variable `JULIA_NUM_THREADS=auto` to let Julia use all CPU threads.

```sh title="~/.profile"
export JULIA_NUM_THREADS=auto
```

### Customize Conda executable location

Point the environment variable `CONDA_JL_HOME` to your Conda path. `Conda.jl` and `PyCall.jl` will take the preinstalled Conda instead of downloading a standalone one. For example,

```sh title="~/.profile"
export CONDA_JL_HOME="${HOME}/conda"
```

For `PythonCall.jl`, [set the following environment variables](https://cjdoris.github.io/PythonCall.jl/stable/pythoncall/):

```sh
export JULIA_CONDAPKG_BACKEND="Null"
export JULIA_PYTHONCALL_EXE="${HOME}/conda/bin/python"
```

### Load `Revise.jl` at Julia startup

Add the following lines to `~/.julia/config/startup.jl` after `Revise.jl` is installed

```julia title="~/.julia/config/startup.jl"
try
    using Revise
catch e
    @warn "Error initializing Revise" exception=(e, catch_backtrace())
end
```

For `IJulia` (Jupyter notebooks) to use Revise, add the following lines to `~.julia/config/startup_ijulia.jl`

```julia title="~/.julia/config/startup_ijulia.jl"
try
    @eval using Revise
catch e
    @warn "Error initializing Revise" exception=(e, catch_backtrace())
end
```

Or run the following commands (heredoc in Linux) to create these two files at once

```sh
mkdir -p ~/.julia/config/ && cat >  ~/.julia/config/startup.jl << END
try
    using Revise
catch e
    @warn "Error initializing Revise" exception=(e, catch_backtrace())
end
END

mkdir -p ~/.julia/config/ && cat >  ~/.julia/config/startup_ijulia.jl << END
try
    @eval using Revise
catch e
    @warn "Error initializing Revise" exception=(e, catch_backtrace())
end
END
```
