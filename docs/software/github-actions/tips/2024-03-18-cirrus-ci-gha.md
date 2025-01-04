---
title: Github Action and Cirrus CI
date: 2024-03-18
tags:
  - github
  - cirrus-ci
categories:
  - DevOps
---

Run Github actions after successful [Cirrus CI](https://cirrus-ci.org/) runs using the [`check_suite`](https://docs.github.com/en/actions/reference/events-that-trigger-workflows#check_suite) trigger.

<!-- more -->

```yaml title=".github/workflows/cirrus.yml"
on:
  check_suite:
    type: ['completed']

name: Continue after Cirrus CI Completes Successfully
jobs:
  continue:
    name: After Cirrus CI
    if: github.event.check_suite.app.name == 'Cirrus CI' &&  github.event.check_suite.conclusion == 'success'
    runs-on: ubuntu-latest
    steps:
    - name: Continue
      run: echo "Cirrus CI run is Completed"
```
