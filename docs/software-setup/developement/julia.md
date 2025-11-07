---
title: Setup Julia
date: 2025-02-19
tags:
  - julia
  - linux
  - windows
---

## Install Julia

Install Julia with the [juliaup](https://github.com/JuliaLang/juliaup) installer.

=== "Linux/MacOS"

    ```sh
    curl -fsSL https://install.julialang.org | sh -s -- -y
    ```

=== "Windows"

    ```powershell
    winget install julia -s msstore
    ```

    Alternatively, download and install [Julia official binaries](https://julialang.org/downloads/).


## Post-install configurations

### Auto-activate local projects

Set environment variable `JULIA_PROJECT=@.` to let Julia automatically load the closest upstream `Project.toml` and activate the environment.

```sh title="~/.profile"
export JULIA_PROJECT=@.
```

> [!INFO]
> `IJulia.jl`, the Julia kernel for Jupyter notebooks, sets `JULIA_PROJECT=@.` by default. Thus, Jupyter notebooks load their local Julia environments automatically.

> [!WARNING]
> Loading local environments unconditionally is unsafe for untrusted sources, as shown in [Nefarious.jl](https://github.com/StefanKarpinski/Nefarious.jl).
> That is why Julia does not run `julia --project=@.` by default.

### Fully utilize CPU threads

Set environment variable `JULIA_NUM_THREADS=auto` to let Julia utilize all CPU threads.

```sh title="~/.profile"
export JULIA_NUM_THREADS=auto
```

### Run Python packages

To run Python packages in Julia (such as `matplotlib` for `PythonPlot.jl` and `jupyter` for `IJulia.jl`)

1. Install [[developement/python#micromamba|micromamba]], the minimal Python package manager.
2. Create a conda environment, for example, `micromamba create -n juliapy jupyter matplotlib`.
3. Set up the following environment variables
  - `PythonCall.jl` [documentation](https://juliapy.github.io/PythonCall.jl/stable/pythoncall/#pythoncall-config)
  - `Conda.jl` [documentation](https://github.com/JuliaPy/Conda.jl#using-a-pre-existing-conda-installation)

```sh title="~/.profile"
export CONDA_JL_HOME="${HOME}/micromamba/envs/juliapy"
export JULIA_PYTHONCALL_EXE="${CONDA_JL_HOME}/bin/python"
export JULIA_CONDAPKG_BACKEND="Null"
```

### Load packages at REPL startup

Add the following lines to `~/.julia/config/startup.jl` after `Revise.jl` and `OhMyREPL.jl` are installed

```julia title="~/.julia/config/startup.jl"
using Pkg: Pkg
if isinteractive()
    using OhMyREPL
    using Revise
    catch e
        @warn "Error initializing" exception=(e, catch_backtrace())
        @info "Try to install OhMyREPL and Revise"
        Pkg.add(["OhMyREPL", "Revise"])
    end
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
using Pkg: Pkg
if isinteractive()
    using OhMyREPL
    using Revise
    catch e
        @warn "Error initializing" exception=(e, catch_backtrace())
        @info "Try to install OhMyREPL and Revise"
        Pkg.add(["OhMyREPL", "Revise"])
    end
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
