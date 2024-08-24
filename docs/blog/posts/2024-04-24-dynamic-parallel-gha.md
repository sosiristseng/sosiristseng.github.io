---
title: Dynamic parallel matrix
date: 2024-04-24
tags:
  - github
categories:
  - DevOps
---

[Job matrix](https://docs.github.com/en/actions/using-jobs/using-a-matrix-for-your-jobs) creates multiple job runs that are based on the combinations of the variables. Sometimes we want a dynamic number of matrix jobs, which requires a JSON array as an output. Here we use `json` and `glob` modules in Python to generate that JSON list.[^list-in-dir][^ls-json]

<!-- more -->

[^list-in-dir]: https://stackoverflow.com/questions/3207219/how-do-i-list-all-files-of-a-directory
[^ls-json]: https://stackoverflow.com/questions/10234327/convert-bash-ls-output-to-json-array

```yaml
name: Show text files with dynamic parallel matrix

on:
  push:
    branches:
    - main

jobs:
  setup:
    runs-on: ubuntu-latest
    outputs:
      matrix: ${{ steps.set-matrix.outputs.matrix }}
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3
      - name: List text files as a JSON array
        id: set-matrix
        run: echo "matrix=$(python -c 'import glob, json; print(json.dumps(glob.glob("*.txt")))')" >> $GITHUB_OUTPUT
  execute:
    needs: setup
    strategy:
      fail-fast: false
      matrix:
        textfile: ${{ fromJSON(needs.setup.outputs.matrix) }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3
      - name: Print text file
        run: cat ${{ matrix.textfile }}
```
