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

The https://github.com/actions/setup-python actions installs `python` with a specific version and could cache downloaded Python packages. (But *not* the installed environment)

```yaml
steps:
- uses: actions/checkout@v4
- uses: actions/setup-python@v5
  with:
    python-version: '3.x'
    cache: 'pip'
- run: pip install -r requirements.txt
```

### Cache virtual environment

The following workflow caches the virtual environment folder[^2], which is faster than caching the whole Python environment.

```yaml
- name: Setup Python
  uses: actions/setup-python@v5
  id: setup-python
  with:
    python-version: '3.x'
- name: Cache virtualenv
  uses: actions/cache@v4
  id: cache-venv
  with:
    key: ${{ runner.os }}-venv-${{ steps.setup-python.outputs.python-version }}-${{ hashFiles('requirements.txt') }}
    path: .venv
- name: Install Python dependencies
  run: |
    python -m venv .venv
    source .venv/bin/activate
    python -m pip install -r requirements.txt
    echo ".venv/bin" >> $GITHUB_PATH
    echo "VIRTUAL_ENV=.venv" >> $GITHUB_ENV
    echo "PYTHON=${VIRTUAL_ENV}/bin/python" >> $GITHUB_ENV
    echo "JULIA_PYTHONCALL_EXE=${VIRTUAL_ENV}/bin/python">> $GITHUB_ENV
```

[^2]: https://adamj.eu/tech/2023/11/02/github-actions-faster-python-virtual-environments/

### Use `uv`

[uv](https://docs.astral.sh/uv/) is a drop-in replacement for `pip`, an extremely fast Python package and project manager written in Rust.

The GitHub actions [workflow](https://docs.astral.sh/uv/guides/integration/github/):

```yaml
name: UV example

jobs:
  python-linux:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.x'
      - name: Set up uv
        run: curl -LsSf https://astral.sh/uv/install.sh | sh
      - name: Install requirements
        run: uv pip install --system -r requirements.txt
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
