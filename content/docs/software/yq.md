---
title: yq
tags:
  - python
  - yaml
---

Editing YAML files on-the-fly with https://github.com/mikefarah/yq.

<!--more-->

For example, to disable jupyter book cell execution in GitHub actions, one can edit `docs/_config.yml` and set `execute_notebooks` to `off`.

```yaml
- name: Disable code cell execution
  uses: mikefarah/yq@master
  with:
    cmd: yq -i '.execute.execute_notebooks = "off"' 'docs/_config.yml'
```
