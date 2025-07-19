---
title: Julia in GitHub actions
date: 2024-04-25
tags:
  - github
  - julia
---

## Official Julia GitHub actions

- https://github.com/julia-actions/setup-julia action downloads `julia` and adds it to `PATH`.
- https://github.com/julia-actions/julia-buildpkg runs build scripts and installs dependencies for the Julia package.
- https://github.com/julia-actions/julia-runtest runs unit test for the Julia project.
- https://github.com/julia-actions/cache is a shortcut action to cache Julia artifacts, packages, and registries.
- https://github.com/julia-actions/julia-docdeploy deploys documentation.
- https://github.com/julia-actions/julia-processcoverage generates test coverage data.

<!-- more -->

Example workflow:

```yaml
name: CI

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - uses: julia-actions/setup-julia@v1
    - uses: julia-actions/cache@v1
    - uses: julia-actions/julia-buildpkg@v1
    - uses: julia-actions/julia-runtest@v1
    - uses: julia-actions/julia-docdeploy@v1
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        DOCUMENTER_KEY: ${{ secrets.DOCUMENTER_KEY }}
    - uses: julia-actions/julia-processcoverage@v1
    - uses: codecov/codecov-action@v2
      with:
        files: lcov.info
```

## Using the Julia shell

Using Julia shell to run Julia scripts is much cleaner than `julia -e 'code'`.[^juliashell]

For example, the two steps do the same:

```yaml
- name: Run Julia command
  shell: julia --color=yes --project=. --threads=auto {0}
  run: |
    println("Hello, Julia!")
    println("This is fine.")

- name: Run Julia command
  run: julia --color=yes --project=. --threads=auto -e '
    println("Hello, Julia!")
    println("This is fine.")'
```

[^juliashell]: https://discourse.julialang.org/t/tip-use-julia-as-custom-shell-in-github-actions/53377

## Using PyCall.jl

In GNU/Linux systems like Ubuntu, `PyCall.jl` may not be able to install python packages for `PyCall.jl` because it will first try to use the system Python (`/usr/bin/python`) and `pip`. It would fail due to lack of superuser privileges.

To solve this, you can set the `PYTHON` environment variable to where the Python executable is.[^pycalljldocs]

- Either using a blank (`PYTHON:''`) variable will force Julia to install a local miniconda distribution.
- Or using the Python executable from the [`setup-python` action](https://github.com/marketplace/actions/setup-python).

[^pycalljldocs]: [PyCall.jl documentation](https://github.com/JuliaPy/PyCall.jl#specifying-the-python-version)

```yaml
- uses: actions/setup-python@v4
  id: py
  with:
    python-version: '3.x'
- uses: julia-actions/setup-julia@v1
  with:
    version: 1
- uses: julia-actions/julia-buildpkg@v1
  env:
    # PYTHON: ''      # Use python from Conda.jl
    PYTHON: ${{ steps.py.outputs.python-path }}  # Use python from setup-python
```
