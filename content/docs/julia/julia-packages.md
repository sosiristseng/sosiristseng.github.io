---
title: Julia packages list
tags:
- julia
---

<!--more-->

## Package development

- https://github.com/invenia/PkgTemplates.jl : templates to create new Julia packages.
- https://github.com/timholy/Revise.jl : reducing the need to restart when you make changes to code.
- https://github.com/Roger-luo/FromFile.jl : including other files without duplication.
- https://github.com/wookay/Jive.jl : unit testing in parallel.
- https://github.com/JuliaTesting/TestEnv.jl : Activate your test environment, so you can use your test dependencies locally.

## Publishing code examples

- https://github.com/fredrikekre/Literate.jl : converting _literated_ `jl` files to Markdown (`md`) or Jupyter notebooks (`ipynb`).
- https://github.com/JuliaDocs/Documenter.jl : generating package documentation.
- https://github.com/PumasAI/QuartoNotebookRunner.jl : run [Quarto](https://quarto.org/) notebooks containing Julia code and save the results to Jupyter notebooks.
- https://github.com/stevengj/NBInclude.jl : converting Jupyter notebooks (`ipynb`) to _literated_ `jl` files by using `nbexport("myfile.jl", "myfile.ipynb")`.

## Optimization

- https://github.com/baggepinnen/Hyperopt.jl : Hyperparameter optimization for every cost function with multiprocessing and multithreading support.
- https://github.com/SciML/Optimization.jl : A unified interface for [various optimizers](https://docs.sciml.ai/Optimization/stable/#Overview-of-the-Optimizers)
    - `OptimizationBBO` for black-box optimization from https://github.com/robertfeldt/BlackBoxOptim.jl
    - `OptimizationEvolutionary` for genetic algorithm from https://github.com/wildart/Evolutionary.jl
    - `OptimizationOptimJL` for optimization methods from https://github.com/JuliaNLSolvers/Optim.jl
    - `OptimizationMOI` for optimization methods from https://github.com/jump-dev/MathOptInterface.jl
    - etc.

### Curve fitting and parameter estimation

- https://github.com/JuliaNLSolvers/LsqFit.jl
- https://github.com/SciML/DiffEqParamEstim.jl : small parameter estimation problems.
- https://github.com/sebapersson/PEtab.jl : create parameter estimation problems for ODE models. Might replace `DiffEqParamEstim.jl`.
- https://github.com/SciML/SciMLSensitivity.jl : big parameter estimation problems.

## Modeling and simulation

- https://github.com/SciML/DifferentialEquations.jl : solving differential equations.
- https://github.com/SciML/ModelingToolkit.jl : a symbolic-numeric modeling framework based on https://github.com/JuliaSymbolics/Symbolics.jl, a computer algebra system (CAS) for symbolic calculations.
- https://github.com/SciML/Catalyst.jl : a domain-specific language (DSL) for chemical reaction networks based on https://github.com/SciML/ModelingToolkit.jl.
- https://github.com/JuliaDynamics/Agents.jl : agent-based modeling (ABM).

### Universal differential equations (UDEs)

Neural network x differential equations

- https://github.com/SciML/DiffEqFlux.jl : solving differential equations with neural networks.
- https://github.com/SciML/NeuralPDE.jl : Physics-Informed Neural Networks (PINNs).

### Partial differential equations (PDEs)

- https://github.com/SciML/MethodOfLines.jl : finite difference method (FDM).
- https://github.com/Ferrite-FEM/Ferrite.jl : finite element method (FEM).
- https://github.com/gridap/Gridap.jl : grid-based approximation of PDEs with an expressive API.
- https://github.com/trixi-framework/Trixi.jl : hyperbolic PDE solver.
- https://github.com/WIAS-PDELib/VoronoiFVM.jl : finite volume method (FVM).

### Model analysis

- https://github.com/bifurcationkit/BifurcationKit.jl : bifurcation analysis.

## Probability and Statistics

- https://github.com/JuliaStats/StatsBase.jl : statistics-related functions.
- https://github.com/JuliaStats/GLM.jl : Generalized linear models (GLMs).

## Handy tools

- https://github.com/JuliaMath/Interpolations.jl : continuous interpolation of discrete datasets.
- https://github.com/SciML/DataInterpolations.jl : A library of data interpolation and smoothing functions.
- https://github.com/korsbo/Latexify.jl : convert julia objects to LaTeX equations.
- https://github.com/devmotion/SimpleUnPack.jl : Lightweight Julia macro `@unpack a,b = obj` for destructuring properties and fields.

## Arrays

- https://github.com/JuliaArrays/LazyGrids.jl : multi-dimensional grids.
- https://github.com/jonniedie/ComponentArrays.jl : arrays with arbitrarily nested named components.

## Visualization

- https://github.com/JuliaPlots/Plots.jl : a unified interface for various visualization libraries.
- https://github.com/stevengj/PythonPlot.jl : `matplotlib.pyplot` in Julia, using https://github.com/cjdoris/PythonCall.jl for python libraries.
- https://github.com/MakieOrg/Makie.jl : native Julia visualizations with GPU acceleration and an interactive interface.

## Concurrency

[Julia docs: Parallel Computing](https://docs.julialang.org/en/v1/manual/parallel-computing/)

- https://github.com/JuliaFolds/Folds.jl : a unified interface for sequential, threaded, and distributed fold.
- https://github.com/JuliaFolds2/OhMyThreads.jl : Simple multithreading in Julia.
