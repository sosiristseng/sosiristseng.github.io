---
title: Strip Jupyter Notebook Output
draft: false
tags:
  - python
  - jupyter-notebook
  - git
  - devops
---

Jupyter notebooks without multimedia outputs are more friendly to source control since git is not good at comparing binary data (e.g., plots, pictures, videos) in jupyter notebooks. And they tend to bloat the size of git repositories.

## Using nbconvert

You can use `nbconvert` to remove the output cells of Jupyter notebooks.

```bash

jupyter nbconvert --clear-output --inplace my_notebook.ipynb

```

### Git automation

YOu can use Git automation to strip the output automatically on git commit. The following git filter settings keep full notebooks as-is but commit the "clean" version.

In your project folder's `.git/config`:

```gitconfig title=".git/config"
[filter "strip-notebook-output"]
    clean = "jupyter nbconvert --clear-output --inplace --stdin --stdout --log-level=ERROR"
```

And in your project folder's `.gitattributes`:

```gitattributes title=".gitattributes"
*.ipynb filter=strip-notebook-output
```

How this works: [^1]

- The `attribute` tells git to run the filter's clean action on each notebook file before adding it to the index (staging).
- The filter is our friend `nbconvert`, set up to read from stdin, write to stdout, strip the output, and only speak when it has something important to say.
- When a file is extracted from the index, the filter's smudge action is run, but this is a no-op as we did not specify it. You could run your notebook here to re-create the output (`nbconvert --execute --inplace`).
- Note that if the filter somehow fails, the file will be staged unconverted.

[^1]: <https://stackoverflow.com/questions/28908319/how-to-clear-jupyter-notebooks-output-in-all-cells-from-the-linux-terminal>

## nbstripout

[nbstripout](https://github.com/kynan/nbstripout) is a python package to automate these works above.

## nbstripout-fast

[nbstripout-fast](https://github.com/stas00/jupyter-notebook-tools/blob/master/nbstripout/nbstripout-fast) is a simple python script that runs much faster than `nbconvert --clear-output`.

In your project folder's `.git/config`:

```gitconfig title=".git/config"
[filter "nbstripout"]
  clean = nbstripout-fast
    # smudge = cat
    # required = true
[diff "ipynb"]
    textconv = nbstripout-fast -t
```

And in your project folder's `.gitattributes`:

```gitconfig title=".gitattributes"
[filter "nbstripout"]
  clean = nbstripout-fast
    # smudge = cat
    # required = true
[diff "ipynb"]
    textconv = nbstripout-fast -t
```
