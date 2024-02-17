---
title: Cancel old jobs
tags:
  - git
  - github
  - devops
---

The [concurrency](https://docs.github.com/en/actions/using-jobs/using-concurrency) keyword ensures there is only one job running on the specified group. If there are older jobs running in the same group, you could  cancel old jobs to save runner resources.

```yaml
concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true
```
