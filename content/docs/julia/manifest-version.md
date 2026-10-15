---
title: Parse Julia version
date: 2024-03-21
tags:
  - python
  - toml
  - julia
---

<!--more-->

## Python

Use `pathlib` to read and `tomllib` to parse `julia_version` from `Manifest.toml`. (requires Python >= 3.11)

```python
import tomllib; from pathlib import Path; print(tomllib.loads(Path("Manifest.toml").read_text())["julia_version"])
```

And it's easy to run in a bash shell,

```sh
python -c 'import tomllib; from pathlib import Path; print(tomllib.loads(Path("Manifest.toml").read_text())["julia_version"])'
```

In GitHub actions,

```sh
echo "resolved=$(python -c 'import tomllib; from pathlib import Path; print(tomllib.loads(Path("Manifest.toml").read_text())["julia_version"])')" >> "$GITHUB_OUTPUT"
```

## Bash

Use `awk` to parse `julia_version` from `Manifest.toml`.

```sh
echo "resolved=$(awk -F '"' '/^[[:space:]]*julia_version/ {print $2}' Manifest.toml)" >> "$GITHUB_OUTPUT"
```
