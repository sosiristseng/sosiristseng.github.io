---
title: GitHub actions
tags:
  - git
  - github
  - devops
---

[GitHub actions](https://docs.github.com/en/actions) CI/CD. See also https://github.com/sdras/awesome-actions for a curated topics about GitHub actions.

## Build

+ [[git-ops-gha|Git operations in GitHub actions]]
+ [[caching-gha|Caching in GitHub actions]]. Some programming languages might already implemented their own caching actions in their respective "setup" actions.
+ [[dynamic-parallel-gha|Dynamic parallel matrix]]

### Cancel old jobs

The [concurrency](https://docs.github.com/en/actions/using-jobs/using-concurrency) keyword ensures there is only one job running on the specified group. If there are older jobs running in the same group, you could  cancel old jobs to save runner resources.

```yaml
concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true
```

### Artifacts

- The [upload-artifact](https://github.com/actions/upload-artifact) and the [download-artifact](https://github.com/actions/download-artifact) actions by GitHub for storing and retrieving workflow generated data in **the same workflow**.
- The [action-download-artifact](https://github.com/dawidd6/action-download-artifact) action downloads and extracts uploaded artifact(s) associated with a **given (different) workflow**.

  ```yaml
  - name: Download artifact
    uses: dawidd6/action-download-artifact@v2
    with:
      # Optional, GitHub token, a Personal Access Token with `public_repo` scope if needed
      # Required, if artifact is from a different repo
      # Required, if repo is private a Personal Access Token with `repo` scope is needed
      github_token: ${{secrets.GITHUB_TOKEN}}
      # Required, workflow file name or ID
      workflow: workflow_name.yml
      # Optional, uploaded artifact name,
      # will download all artifacts if not specified
      # and extract them in respective subdirectories
      # https://github.com/actions/download-artifact#download-all-artifacts
      name: artifact_name
      # Optional, directory where to extract artifact(s), defaults to current directory
      path: extract_here
  ```

- The [artifacts-url-comments](https://github.com/tonyhallett/artifacts-url-comments) action creates comment(s) in pull request and/or associated issues containing the URL to artifacts from the workflow run being watched.


## Release

[[pages-gha|GitHub pages]]

### GitHub releases

+ https://github.com/softprops/action-gh-release : A GitHub Action for creating GitHub Releases on Linux, Windows, and macOS virtual environments.
+ https://github.com/release-drafter/release-drafter : Drafts your next release notes as pull requests are merged into master.
+ https://github.com/robinraju/release-downloader : Github action to download release assets from private or public repositories.
+ https://github.com/actions/delete-package-versions : This action deletes versions of a package from [GitHub Packages](https://github.com/features/packages). This action will only delete a maximum of 100 versions in one run.

## Misc

+ [[cirrus-ci-gha|Collaborate with Cirrus CI]]
+ [[gh-issue-markdown|Backup GitHub issues in Markdown files]] using `gh2md`.
+ https://github.com/actions/stale : Marks issues and pull requests that have not had recent interaction as stale and might close them after a while.
