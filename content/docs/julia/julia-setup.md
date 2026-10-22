---
title: Julia setup
tags:
  - julia
  - development
---

## Install Julia

Using the [juliaup](https://github.com/JuliaLang/juliaup) installer.

### Linux/MacOS

```sh
curl -fsSL https://install.julialang.org | sh -s -- -y
```

### Windows

```powershell
winget install julia -s msstore
```

## Post-install configurations

### Auto-activate local projects

Set environment variable `JULIA_PROJECT=@.` to let Julia automatically load the closest upstream `Project.toml` and activate the environment.

```sh {filename="~/.profile"}
export JULIA_PROJECT=@.
```

> [!NOTE]
> `IJulia.jl`, the Julia kernel for Jupyter notebooks, sets `JULIA_PROJECT=@.` by default. Thus, Jupyter notebooks load their local Julia environments automatically.

> [!WARNING]
> Loading local environments unconditionally is unsafe for untrusted sources, as shown in [Nefarious.jl](https://github.com/StefanKarpinski/Nefarious.jl).
> That is why Julia does not do `julia --project=@.` by default.

### Fully utilize CPU threads

Set environment variable `JULIA_NUM_THREADS=auto` to let Julia utilize all CPU threads.

```sh {filename="~/.profile"}
export JULIA_NUM_THREADS=auto
```

### Run Python packages

- `PythonCall.jl` [documentation](https://juliapy.github.io/PythonCall.jl/stable/pythoncall/#pythoncall-config)
- `CondaPkg.jl` [documentation](https://github.com/JuliaPy/CondaPkg.jl#preferences)

You can install Python dependencies into a common environment in `~/.julia/conda_environments/mpl` by setting the following environment variable.

```sh {filename="~/.profile"}
export JULIA_CONDAPKG_ENV="@mpl"
```

### Persistent session

Using [JuliaDaemon.jl](https://github.com/KristofferC/JuliaDaemon.jl) to keep persistent Julia sessions to avoid package load and JIT compile latency. Useful for AI agents.

You might need to add `~/.julia/bin` to your `PATH`:

```sh {filename="~/.profile"}
# set PATH so it includes Julia APPs if it exists
if [ -d "$HOME/.julia/bin" ] ; then
    PATH="$HOME/.julia/bin:$PATH"
fi
```

To install it as a Pkg app and register the agent skill:

In Julia session:

```julia
pkg> app add https://github.com/KristofferC/JuliaDaemon.jl
```

In bash/zsh, run

```sh
$jld install
```

Then AI agent will read the skill and use `jld` to run Julia scripts.

### See also

- [Kaimon.jl](https://github.com/kahliburke/Kaimon.jl) for more sophisticated Julia MCP tools (code execution, introspection, debugging, testing, and semantic search).
