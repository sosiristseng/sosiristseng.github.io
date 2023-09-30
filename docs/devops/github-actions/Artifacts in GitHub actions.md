---
title: Artifacts in GitHub actions
tags:
  - github
  - devops
---
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