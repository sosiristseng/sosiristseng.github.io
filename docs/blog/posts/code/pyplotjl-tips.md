---
title: PyPlot.jl tips
date: 2024-04-04
tags:
  - julia
  - visualization
  - tiff
---

Some tips about https://github.com/JuliaPy/PyPlot.jl, the `matplotlib` (Python) visualization library for Julia. See also [docs for matplotlib](https://matplotlib.org/) since `PyPlot.jl` largely follows `matplotlib`'s API.

## How to solve `PyPlot.jl` installation errors

Since `PyPlot.jl` depends on the Python package `matplotlib`, sometimes simply `]add` the package will not work due to some quirks in the installation process.

In a local computer, it is recommended to have a clean [Conda environment inside Julia](https://github.com/JuliaPy/Conda.jl) to minimize issues. To enforce a local miniconda environment inside Julia, set the `PYTHON` environment variable to an empty string.

```julia title="~/.julia/config/startup.jl"
ENV["PYTHON"]=""
```

And then rebuild related packages.

```julia
import Pkg
Pkg.build(["PyCall", "Conda", "PyPlot"])

# should download conda and matplotlib and import PyPlot
using PyPlot
```

## How to share the legend box in double y axis

- Capture line plot objects from both axes.
- Call `legend()` for both(all) line plot objects.

```julia
import PyPlot as plt
x1 = 1:10

fig, ax1 = plt.subplots()
l1 = ax1.plot(x1, x1)
ax2 = ax1.twinx()
l2= ax2.plot(x1, exp.(x1))
ax1.legend([first(l1), first(l2)], ["x", "exp(x)"])
```

## How to save as TIFF image

Exporting `pyplot` figures to TIFF images with a higher dpi and LZW compression.

`PyPlot.jl`

```julia
fig.savefig("fig.tif", dpi=300, pil_kwargs=Dict("compression" => "tiff_lzw"))
```

`PythonPlot.jl`

```julia
using PythonCall
plt.savefig("fig1.tif", dpi=300, pil_kwargs=pydict(Dict("compression" => "tiff_lzw")))
```

## Change default options in PyPlot.jl

Changing [mplstyle and rcparams](https://matplotlib.org/stable/tutorials/introductory/customizing.html) in `matplotlib`.

Sources:
1. [mplstyle and rcparams](https://matplotlib.org/stable/tutorials/introductory/customizing.html) for matplotlib
2. [PyPlot.jl](https://github.com/JuliaPy/PyPlot.jl) readme
3. [mplstyle and rcparams](https://matplotlib.org/stable/tutorials/introductory/customizing.html) in `matplotlib` docs.

### Python

`matplotlib`

```python
import matplotlib as mpl
mpl.rcParams["font.sans-serif"] = "Arial"
mpl.rcParams["font.family"] = "sans-serif"
mpl.rcParams["font.size"] = 12
```
### Julia

`PyPlot.jl`

```julia
import PyPlot as plt
rcParams = plt.PyDict(plt.matplotlib."rcParams")
rcParams["font.sans-serif"] = "Arial"
rcParams["font.family"] = "sans-serif"
rcParams["font.size"] = 12
```

For `Plots.jl`, there is an internal `pyrcparams` dictionary for the `pyplot`(`matplotlib`) backend.

```julia
using Plots
Plots.pyplot()
Plots.pyrcparams["font.size"] = 12
Plots.pyrcparams["font.sans-serif"] = "Arial"
Plots.pyrcparams["font.family"] = "sans-serif"
```

`PythonPlot.jl`

```julia
import PythonPlot as plt
plt.matplotlib.rcParams["font.size"] = 14
```
