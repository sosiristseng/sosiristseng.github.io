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
+ https://github.com/conda-incubator/setup-miniconda
+ https://github.com/mamba-org/setup-micromamba

## Pip packages

The https://github.com/actions/setup-python actions installs `python` with a specific version and could cache download Python packages. (But *not* the whole environment)

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

If you really want to cache the whole Python environment, cache the `pythonLocation` folder.[^1][^2]

```yaml
- name: Set up Python
  uses: actions/setup-python@v4
  id: cp
  with:
    python-version: ${{ matrix.python-version }}
- name: Cache pip dependencies
  uses: actions/cache@v3
  id: cache
  with:
    path: ${{ env.pythonLocation }}
    key:  ${{ runner.os }}-pip-${{ steps.cp.outputs.python-version }}-${{ hashFiles('requirements.txt') }}
- name: Install pip dependencies if cache miss
  if: ${{ steps.cache.outputs.cache-hit != 'true' }}
  run: pip install -r requirements.txt
```

[^1]: https://github.com/actions/setup-python/issues/330#issuecomment-1416883170
[^2]: https://luminousmen.com/post/making-ci-workflow-faster-with-github-actions

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

### Miniconda action

The https://github.com/conda-incubator/setup-miniconda action sets up a base [`conda`](https://docs.conda.io/projects/conda/en/latest/) environment.

```yaml
jobs:
  mambaforge-example:
    runs-on: "ubuntu-latest"
    defaults: # (1)!
      run:
        shell: bash -l {0}
    steps:
      - uses: actions/checkout@v3
      - name: Setup Mambaforge
        uses: conda-incubator/setup-miniconda@v2
        with:
          auto-update-conda: true
          environment-file: environment.yml
          conda-solver: libmamba
      - run: |
          conda info
          conda list
```

1. Use the login shell to activate the conda environment correctly.
