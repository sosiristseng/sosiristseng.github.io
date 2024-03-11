---
title: Status check for a multi-stage workflow
tags:
  - github
  - devops
---

If you run a multi-stage workflow with [status checks](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/collaborating-on-repositories-with-code-quality-features/about-status-checks) in [branch protection rules](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/managing-a-branch-protection-rule), you might found that **skipped jobs are treated as "passed"**. That is, if you have a workflow with a chain of three dependent jobs A -> B -> C. When B fails and C is skipped, it still counts as passed if we only check job C.[^1] This behavior may make us merge broken code. We could list all A, B, and C jobs as required jobs, but this is tedious and could not be done in [dynamic matrix](dynamic-parallel-gha.md). But there is a workaround. We could add an additional job that is always executed and bails out when the required job is not successful. The branch protection rules can depend on this job to determine whether this workflow is successful or not.

[^1]: https://brunoscheufler.com/blog/2022-04-09-the-required-github-status-check-that-wasnt

```yaml
jobs:
  stage1:
    runs-on: ubuntu-latest
    steps:
    # Run steps...
  stage2:
    needs: stage1
    runs-on: ubuntu-latest
    steps:
    # Run steps...
  stage3:
    needs: stage2
    runs-on: ubuntu-latest
    steps:
    # Run steps...
  # CI conclusion for GitHub status check
  # Adapted from https://brunoscheufler.com/blog/2022-04-09-the-required-github-status-check-that-wasnt
  CI:
    needs: stage3
    if: always()
    runs-on: ubuntu-latest
    steps:
      - run: |
          if [[ ${{ needs.stage3.result }} == "success" ]]; then
            echo "Tests passed"
            exit 0
          else
            echo "Tests failed"
            exit 1
          fi
```
