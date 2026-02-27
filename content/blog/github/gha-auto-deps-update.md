---
title: Automatic Dependency Update in GitHub
date: 2025-02-19
tags:
  - github
---

Updating package dependencies automatically as a part of continuous integration (CI).

<!--more-->

## Dependabot

[Dependabot](https://docs.github.com/en/code-security/dependabot) creates a pull request once there is an update for the dependencies. The pull requests are usually tested by continuous integration (CI).

However, [dependabot does not support automerging on its own](https://github.blog/changelog/2021-02-19-github-actions-workflows-triggered-by-dependabot-prs-will-run-with-read-only-permissions/) due to security concerns. The good news is that we could use [Kodiak](https://kodiakhq.com/) to do the job. See it's [quickstart](https://kodiakhq.com/#quickstart) if you are interested.

For example, the dependabot file `.github/dependabot.yml`

```yaml {filename=".github/dependabot.yml"}
version: 2

updates:
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "daily"
    labels:
    - "automerge"
```

Kodiak bot file: `.github/.kodiak.toml`

```toml {filename=".github/.kodiak.toml"}
version = 1

[merge]
method = "squash"
```

And you need additional steps in the Github settings to make Kodiak Bot work

- Add the `automerge` tag in the GitHub issue tab.
- In `Options` -> `Branches`, protect the to-be-merged branch (usually the `main` branch)
  - Also tick "Require status checks to pass before merging" and "Require branches to be up to date before merging"
  - And select which github action job(s) should be passed in order to automerge by using the search bar below.

## Renovate

[Renovate bot](https://docs.renovatebot.com/) can manage both dependency update checking and automated pull request merging.

Renovate supports a variety of platforms

- GitHub (.com and Enterprise)
- GitLab (.com and CE/EE)
- Bitbucket Cloud / Servee
- Azure DevOps
- Gitea

And a variety of programming languages

- Git submodules
- GitHub actions
- Node JS packages
- Dockerfile
- Javascript (and node JS)
- Java
- And more

### Setup for GitHub

Enable the [Renovate GitHub APP](https://github.com/marketplace/renovate) for GitHub repositories. Renovate bot will open an pull request for reachable repos to begin an interactive setup.

### Setup for GitLab

According to the [renovate GitLab runner documentation](https://gitlab.com/renovate-bot/renovate-runner/),

1. Create a repository for the Renovate runner.
2. Add a GitLab [personal access token (PAT)](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html#creating-a-personal-access-token) with `read_user`, `api` and `write_repository` scopes as the `RENOVATE_TOKEN` CI/CD variable,
3. Add a [GitHub PAT](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/creating-a-personal-access-token) as `GITHUB_COM_TOKEN`. This token allows renovate bot to read information of updated dependencies unhindered.
4. Create `.gitlab-ci.yml` to run the pipelines
    ```yaml {filename=".gitlab-ci.yml"}
    include:
     - project: 'renovate-bot/renovate-runner'
       file: '/templates/renovate-dind.gitlab-ci.yml'
    ```
5. Select what repositories renovate bot could touch by setting up the CI/CD variable `RENOVATE_EXTRA_FLAGS` : `--autodiscover=true --autodiscover-filter=group1/*` or configure them in the `config.js` file.
    ```js {filename="config.js"}
    module.exports = {
        repositories: [
            "group1/repo1",
            "group2/repo2",
        ],
    };
    ```
    As a plus, it's easier to set up more renovate runner options in the `config.js` file.
6. Setup a [schedule](https://docs.gitlab.com/ee/ci/pipelines/schedules.html) for the pipeline.

### Renovate settings file

The settings file `renovate.json` example

```json {filename="renovate.json"}
{
  "extends": [
    "config:recommended",
  ],
  "git-submodules": {
      "enabled": true
  }
}
```
