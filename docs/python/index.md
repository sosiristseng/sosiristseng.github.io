---
title: Python Tips
tags:
  - python
---

## Change Jupyter book build options on-the-fly

You can edit the build options file `_config.yml` on-the-fly using the [`yq` tool](https://github.com/mikefarah/yq).

For example, to disable notebook cell execution in github actions:

```yaml
- name: Disable code cell execution
  uses: mikefarah/yq@master
  with:
    cmd: yq -i '.execute.execute_notebooks = "off"' 'docs/_config.yml'
```
