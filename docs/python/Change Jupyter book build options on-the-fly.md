---
title: Change Jupyter book build options on-the-fly
draft: false
tags:
  - python
  - github
  - jupyter-notebook
---

You can edit `_config.yml` on-the-fly using the [`yq` tool](https://github.com/mikefarah/yq) to change the build options of  [Jupyter book](https://jupyterbook.org/en/stable/).

For example, to disable notebook cell execution in github actions:

```yaml
- name: Disable code cell execution
  uses: mikefarah/yq@master
  with:
    cmd: yq -i '.execute.execute_notebooks = "off"' 'docs/_config.yml'
```