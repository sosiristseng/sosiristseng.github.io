---
title: Github Action and Cirrus CI
draft: false
tags:
  - github
  - devops
  - cirrus-ci
---

Run Github actions after successful [Cirrus CI](https://cirrus-ci.org/) runs using the [`check_suite`](https://docs.github.com/en/actions/reference/events-that-trigger-workflows#check_suite) trigger.

The example workflow file:

```yaml
on:
  check_suite:
    type: ['completed']

name: Continue after Cirrus CI Complets Successfully
jobs:
  continue:
    name: After Cirrus CI
    if: github.event.check_suite.app.name == 'Cirrus CI' &&  github.event.check_suite.conclusion == 'success'
    runs-on: ubuntu-latest
    steps:
    - name: Continue
      run: echo "Cirrus CI run is Completed"
```
