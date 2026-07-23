---
title: Julia setup
tags:
  - julia
  - development
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
> That is why Julia does not run `julia --project=@.` by default.

### Fully utilize CPU threads

Set environment variable `JULIA_NUM_THREADS=auto` to let Julia utilize all CPU threads.

```sh {filename="~/.profile"}
export JULIA_NUM_THREADS=auto
```

### Run Python packages

- `PythonCall.jl` [documentation](https://juliapy.github.io/PythonCall.jl/stable/pythoncall/#pythoncall-config)
- `CondaPkg.jl` [documentation](https://github.com/JuliaPy/CondaPkg.jl#preferences)

Install Python dependencies into a common environment in `~/.julia/conda_environments/mpl`.

```sh {filename="~/.profile"}
export JULIA_CONDAPKG_ENV="@mpl"
```
