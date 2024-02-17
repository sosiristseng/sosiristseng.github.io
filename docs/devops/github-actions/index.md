---
title: GitHub actions
tags:
  - git
  - github
  - devops
---

[GitHub actions](https://docs.github.com/en/actions) CI/CD. See also https://github.com/sdras/awesome-actions for a curated topics about GitHub actions.

## Git repository

[[git-ops-gha|Git Operations in GitHub actions]]

+ Clone: https://github.com/actions/checkout
+ Push changes:
  + https://github.com/EndBug/add-and-commit
  + https://github.com/stefanzweifel/git-auto-commit-action
  + https://github.com/ad-m/github-push-action
+ Pull request: https://github.com/peter-evans/create-pull-request
+ Automerge: https://github.com/peter-evans/enable-pull-request-automerge

## Runtime environment

+ Docker: [[docker-gha]]
+ Pandoc: https://github.com/r-lib/actions/tree/v2-branch/setup-pandoc
+ LaTeX: https://github.com/r-lib/actions/tree/v2/setup-tinytex
+ LaTeX (tectonic): https://github.com/WtfJoke/setup-tectonic
+ Julia: https://github.com/julia-actions/setup-julia
+ NodeJS: https://github.com/actions/setup-node
+ Python: https://github.com/actions/setup-python / https://github.com/mamba-org/setup-micromamba

## Build

+ [[artifacts-gha|Artifacts]]
+ [[caching-gha|Caching in GitHub actions]]. Some programming languages might already implemented their own caching actions in their respective "setup" actions.
+ [[cancel-old-jobs|Cancel old jobs]]
+ [[dynamic-parallel-gha|Dynamic parallel matrix]]
+ [[status-check-job|Ensure successful status checks pass CI]]

## Release

+ [[pages-gha|GitHub pages]].
+ https://github.com/softprops/action-gh-release : A GitHub Action for creating GitHub Releases on Linux, Windows, and macOS virtual environments.
+ https://github.com/release-drafter/release-drafter : Drafts your next release notes as pull requests are merged into master.
+ https://github.com/robinraju/release-downloader : Github action to download release assets from private or public repositories.
+ https://github.com/actions/delete-package-versions : This action deletes versions of a package from [GitHub Packages](https://github.com/features/packages). This action will only delete a maximum of 100 versions in one run.

## Misc

+ [[cirrus-ci-gha|Collaborate with Cirrus CI]]
+ [[gh-issue-markdown|Backup GitHub issues in Markdown files]]
+ https://github.com/actions/stale : Marks issues and pull requests that have not had recent interaction as stale and might close them after a while.
