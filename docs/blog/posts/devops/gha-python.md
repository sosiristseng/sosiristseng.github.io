---
title: Python in GitHub actions
date: 2024-04-25
tags:
  - github
  - conda
  - python
---

+ https://github.com/actions/setup-python
+ https://github.com/mamba-org/setup-micromamba

## Pip packages

The https://github.com/actions/setup-python actions installs `python` with a specific version and could cache downloaded Python packages. (But *not* the installed environment).

[uv](https://docs.astral.sh/uv/) is a drop-in replacement for `pip`, an extremely fast Python package and project manager written in Rust. `uv` caches the environment by default.

```yaml
name: UV example

env:
  UV_SYSTEM_PYTHON: 1

jobs:
  python:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.x'
          check-latest: true
      - name: Install the latest version of uv
        uses: astral-sh/setup-uv@v5
        with:
          version: "latest"
      - name: Install requirements
        run: uv pip install -r requirements.txt
```

## Conda packages

The https://github.com/mamba-org/setup-micromamba action installs the [micromamba](https://github.com/mamba-org/mamba#micromamba) package manager and conda package dependencies. It also caches the Python runtime environment.

```yaml
- uses: mamba-org/setup-micromamba@v1
  with:
    environment-file: environment.yml
    init-shell: bash
    cache-environment: true
    post-cleanup: 'all'

- name: Run custom command in micromamba environment
  shell: micromamba-shell {0}
  run: python --version
```
