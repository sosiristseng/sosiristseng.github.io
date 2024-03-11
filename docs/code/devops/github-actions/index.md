---
title: GitHub actions
tags:
  - git
  - github
  - devops
---

[GitHub actions](https://docs.github.com/en/actions) CI/CD. See also https://github.com/sdras/awesome-actions for a curated topics about GitHub actions.

## Git repository

[Git Operations in GitHub actions](./list-of-github-actions/git-ops-gha.md)

+ Clone: https://github.com/actions/checkout
+ Push changes:
  + https://github.com/EndBug/add-and-commit
  + https://github.com/stefanzweifel/git-auto-commit-action
  + https://github.com/ad-m/github-push-action
+ Pull request: https://github.com/peter-evans/create-pull-request
+ Automerge: https://github.com/peter-evans/enable-pull-request-automerge

## Runtime environment

+ [Docker](./list-of-github-actions/docker-gha.md)
+ Pandoc: https://github.com/r-lib/actions/tree/v2-branch/setup-pandoc
+ LaTeX: https://github.com/r-lib/actions/tree/v2/setup-tinytex
+ LaTeX (tectonic): https://github.com/WtfJoke/setup-tectonic
+ Julia: https://github.com/julia-actions/setup-julia
+ NodeJS: https://github.com/actions/setup-node
+ Python: https://github.com/actions/setup-python / https://github.com/mamba-org/setup-micromamba

## Build

+ [Artifacts](./list-of-github-actions/artifacts-gha.md)
+ [Caching](./list-of-github-actions/caching-gha.md). Some programming languages might already implemented their own caching actions in their respective "setup" actions.
+ [Cancel old jobs](./tips/cancel-old-jobs.md)
+ [Dynamic parallel matrix](./tips/dynamic-parallel-gha.md)
+ [Ensure successful status checks pass CI](./tips/status-check-job.md)

## Release

+ [GitHub pages](./list-of-github-actions/pages-gha.md).
+ https://github.com/softprops/action-gh-release : A GitHub Action for creating GitHub Releases on Linux, Windows, and macOS virtual environments.
+ https://github.com/release-drafter/release-drafter : Drafts your next release notes as pull requests are merged into master.
+ https://github.com/robinraju/release-downloader : Github action to download release assets from private or public repositories.
+ https://github.com/actions/delete-package-versions : This action deletes versions of a package from [GitHub Packages](https://github.com/features/packages). This action will only delete a maximum of 100 versions in one run.

## Misc

+ [GitHub status check with Cirrus CI](./tips/cirrus-ci-gha.md)
+ [Backup GitHub issues in Markdown files](./tips/gh-issue-markdown.md)
+ https://github.com/actions/stale : Marks issues and pull requests that have not had recent interaction as stale and might close them after a while.
