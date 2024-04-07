---
title: "Python: Read TOML file in one line"
date: 2024-03-21
tags:
- python
- julia
- toml
---

Use `pathlib` to read and `tomllib` to parse the file. (requires Python >= 3.11)

For example, to extract Julia version from `Manifest.toml`

```python
import tomllib; from pathlib import Path; print(tomllib.loads(Path("Manifest.toml").read_text())["julia_version"])
```

And it's easy to run in a bash shell or CI script.

```bash
python -c 'import tomllib; from pathlib import Path; print(tomllib.loads(Path("Manifest.toml").read_text())["julia_version"])'
```
