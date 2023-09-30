---
title: Setup Python in GitHub actions
tags:
  - github
  - conda
  - github
  - conda
  - python
draft:
---

## Setup Python environment in GitHub actions

You can use one of the three below
### Setup Python action

The https://github.com/actions/setup-python actions installs `python` with a specific version and (optionally) caches Python package dependencies.

```yaml
steps:
- uses: actions/checkout@v2
- uses: actions/setup-python@v2
  with:
    python-version: '3.x'
    cache: 'pip'
- run: pip install -r requirements.txt
```

### miniconda

The https://github.com/conda-incubator/setup-miniconda action sets up a base [`conda`](https://docs.conda.io/projects/conda/en/latest/) or [mamba](https://github.com/mamba-org/mamba) environment.

```yaml
jobs:
  mambaforge-example:
    runs-on: "ubuntu-latest"
    defaults: # (2)!
      run:
        shell: bash -l {0}
    steps:
      - uses: actions/checkout@v2
      - uses: conda-incubator/setup-miniconda@v2
        with:
          miniforge-variant: Mambaforge  # (1)!
          miniforge-version: latest
          environment-file: environment.yml
          use-mamba: true
      - run: |
          conda info
          conda list
      - run: mamba install jupyterlab
```

1. enables `mamba` by specifying `miniforge-variant` as `Mambaforge`.
2. `bash -l {0}` login shell to activate the conda environment correctly.

### micromamba

The https://github.com/mamba-org/setup-micromamba action installs the [micromamba](https://github.com/mamba-org/mamba#micromamba) package manager.

```yaml
- uses: mamba-org/setup-micromamba@v1
  with:
    environment-file: environment.yml
    init-shell: >-
      bash
      powershell
    cache-environment: true
    post-cleanup: 'all'
```

## Cache python dependencies

### Pip downloads

The https://github.com/actions/setup-python action caches pip downloads.

```yaml
- uses: actions/setup-python@v2
  with:
    python-version: '3.x'
    cache: 'pip'
```

### Python packages

Cache the `pythonLocation` folder to cache installed Python packages.[^1][^2]

```yaml
- name: Set up Python
  uses: actions/setup-python@v4.5.0
  with:
    python-version: ${{ matrix.python-version }}
- name: Cache pip dependencies
  uses: actions/cache@v3.2.4
  id: cache
  with:
    path: ${{ env.pythonLocation }}
    key: ${{ env.pythonLocation }}-${{ hashFiles('requirements.txt') }}
- name: Install pip dependencies
  if: steps.cache.outputs.cache-hit != 'true'
  run: pip install -r requirements.txt
```

[^1]: https://github.com/actions/setup-python/issues/330#issuecomment-1416883170
[^2]: https://luminousmen.com/post/making-ci-workflow-faster-with-github-actions
