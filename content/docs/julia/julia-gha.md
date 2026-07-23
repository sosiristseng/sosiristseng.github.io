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

<!--more-->

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
