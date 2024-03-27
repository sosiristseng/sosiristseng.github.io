---
title: Setup Python
tags:
  - github
  - conda
  - python
  - devops
---

You can use one of the three below

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

### Cache Python environment

If you want to cache the whole Python environment, cache the virtual environment folder.[^1][^2]

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
    key: ${{ runner.os }}-venv-${{ steps.setup-python.outputs.python-version}}-${{ hashFiles('requirements.txt') }}
    path: .venv
- name: Install Python dependencies
  run: |
    python -m venv .venv
    source .venv/bin/activate
    python -m pip install -r requirements.txt
    echo "$VIRTUAL_ENV/bin" >> $GITHUB_PATH
    echo "VIRTUAL_ENV=$VIRTUAL_ENV" >> $GITHUB_ENV
```

[^1]: https://github.com/actions/setup-python/issues/330#issuecomment-1416883170
[^2]: https://adamj.eu/tech/2023/11/02/github-actions-faster-python-virtual-environments/

## Conda packages

### Micromamba

The https://github.com/mamba-org/setup-micromamba action installs the [micromamba](https://github.com/mamba-org/mamba#micromamba) package manager and conda package dependencies. It can also cache the whole runtime environment.

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
