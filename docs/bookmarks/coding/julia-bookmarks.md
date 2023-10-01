---
title: Julia Bookmarks
draft: false
tags:
  - bookmark
  - julia
---
[Gens Julia](https://gensjulia.pages.dev/), the Julia resource list adapted from `Julia.jl`.
## Examples in Jupyter notebooks

- https://github.com/sosiristseng/jl-abm
- https://github.com/sosiristseng/jl-dataframes
- https://github.com/sosiristseng/jl-diffeq
- https://github.com/sosiristseng/jl-pde
- https://github.com/sosiristseng/jl-ude
- https://github.com/sosiristseng/jl-visual

## My Julia stack

### Package development

- [PkgTemplates.jl](https://github.com/invenia/PkgTemplates.jl) : templates to create new Julia packages.
- [Revise.jl](https://github.com/timholy/Revise.jl) : reducing the need to restart when you make changes to code.
- [FromFile.jl](https://github.com/Roger-luo/FromFile.jl) : including other files without duplication.
- [Documenter.jl](https://github.com/JuliaDocs/Documenter.jl) : generating package documentation.
- [Jive.jl](https://github.com/wookay/Jive.jl) : parallel testing.

### Publishing code examples

- [Literate.jl](https://github.com/fredrikekre/Literate.jl) : from _literated_ `jl` files to Markdown (`md`) / Jupyter notebooks (`ipynb`).
- [Weave.jl](https://github.com/JunoLab/Weave.jl) : converting between Markdown (`jmd`), Jupyter notebooks (`ipynb`), and Julia script (`.jl`). It also supports HTML/PDF outputs.
- [NBInclude.jl](https://github.com/stevengj/NBInclude.jl): from Jupyter notebooks (`ipynb`) to _literated_ `jl` files by using `nbexport("myfile.jl", "myfile.ipynb")`.

### Optimization

- [Hyperopt.jl](https://github.com/baggepinnen/Hyperopt.jl) : Hyperparameter optimization for every cost function with multiprocessing and multithreading support.
- [Optimization.jl](https://github.com/SciML/Optimization.jl) : A unified interface for [various optimizers](https://docs.sciml.ai/Optimization/stable/#Overview-of-the-Optimizers)
    - `OptimizationBBO` for black-box optimization from [BlackBoxOptim.jl](https://github.com/robertfeldt/BlackBoxOptim.jl).
    - `OptimizationEvolutionary` for genetic algorithm from [Evolutionary.jl](https://github.com/wildart/Evolutionary.jl).
    - `OptimizationOptimJL` for optimization methods from [Optim.jl](https://github.com/JuliaNLSolvers/Optim.jl).
    - `OptimizationMOI` for optimization methods from [MathOptInterface.jl](https://github.com/jump-dev/MathOptInterface.jl).
    - etc.

### Modeling and simulation

- [DifferentialEquations.jl][]: solving differential eqautions.
- [Symbolics.jl][]: a computer algebra system (CAS) for symbolic calculations.
- [ModelingToolkit.jl][] : a symbolic modeling framework.
- [Catalyst.jl][]: a domain-specific language (DSL) for shemical reaction networks.
- [Agents.jl][]: agent-based modeling (ABM).

[Symbolics.jl]: https://github.com/JuliaSymbolics/Symbolics.jl
[ModelingToolkit.jl]: https://github.com/SciML/ModelingToolkit.jl
[Catalyst.jl]: https://github.com/SciML/Catalyst.jl
[DifferentialEquations.jl]: https://github.com/SciML/DifferentialEquations.jl
[Agents.jl]: https://github.com/JuliaDynamics/Agents.jl

#### Universal differential equations (UDEs)

- [DiffEqFlux.jl][]: solving differential equations with neural networks.
- [NeuralPDE.jl][]: Physics-Informed Neural Networks (PINNs).

[DiffEqFlux.jl]: https://github.com/SciML/DiffEqFlux.jl
[NeuralPDE.jl]: https://github.com/SciML/NeuralPDE.jl

#### Partial differential equations (PDEs)

[Examples](https://sosiristseng.github.io/jl-pde/)

- [MethodOfLines.jl][]: finite difference method (FDM).
- [Ferrite.jl][]: finite element method (FEM).
- [Gridap.jl][]: grid-based approximation of PDEs with an expressive API.
- [Trixi.jl][]: hyperbolic PDE solver.
- [VoronoiFVM.jl][]: finite volume method (FVM).

[MethodOfLines.jl]: https://github.com/SciML/MethodOfLines.jl
[Ferrite.jl]: https://github.com/Ferrite-FEM/Ferrite.jl
[Gridap.jl]: https://github.com/gridap/Gridap.jl
[Trixi.jl]: https://github.com/trixi-framework/Trixi.jl
[VoronoiFVM.jl]: https://github.com/j-fu/VoronoiFVM.jl

#### Model analysis

- [BifurcationKit.jl][]: bifurcation analysis.

[BifurcationKit.jl]: https://github.com/bifurcationkit/BifurcationKit.jl

### Probability and Statistics

- [StatsBase.jl][]: statistics-related functions.
- [GLM.jl][]: Generalized linear models (GLMs).

[GLM.jl]: https://github.com/JuliaStats/GLM.jl
[StatsBase.jl]: https://github.com/JuliaStats/StatsBase.jl

### Handy tools

- [Interpolations.jl][]: continuous interpolation of discrete datasets.
- [Latexify.jl][]: convert julia objects to LaTeX equations.

[Interpolations.jl]: https://github.com/JuliaMath/Interpolations.jl
[Latexify.jl]: https://github.com/korsbo/Latexify.jl

#### Arrays

- [LazyGrids.jl][]: multi-dimensional grids.
- [LabelledArrays.jl][]: a label for each element in a array.
- [ComponentArrays.jl][]: arrays with arbitrarily nested named components.

[LazyGrids.jl]: https://github.com/JuliaArrays/LazyGrids.jl
[LabelledArrays.jl]: https://github.com/SciML/LabelledArrays.jl
[ComponentArrays.jl]: https://github.com/jonniedie/ComponentArrays.jl

### Visualization

- [Plots.jl][]: a unified interface for various visualization libraries.
- [PyPlot.jl][]: `matplotlib.pyplot` in Julia.
- [PythonPlot.jl][]: `matplotlib.pyplot` in Julia, using [PythonCall.jl][] for python libraries.
- [Makie.jl][]: native Julia visualizations.

[Plots.jl]: https://github.com/JuliaPlots/Plots.jl
[PyPlot.jl]: https://github.com/JuliaPy/PyPlot.jl
[PythonPlot.jl]: https://github.com/stevengj/PythonPlot.jl
[PythonCall.jl]: https://github.com/cjdoris/PythonCall.jl
[Makie.jl]: https://github.com/MakieOrg/Makie.jl

### Concurrency

- [Folds.jl][Folds.jl]: a unified interface for sequential, threaded, and distributed fold.
- [ThreadsX.jl][]: multithreaded base functions.

[Folds.jl]: https://github.com/JuliaFolds/Folds.jl
[ThreadsX.jl]: https://github.com/tkf/ThreadsX.jl
