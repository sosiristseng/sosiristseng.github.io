---
title: Git Operations in GitHub actions

tags:
  - git
  - github
  - devops
---

Git commands, such as checkout, add, create a branch, make a pull request in Github actions.

## Checkout (Clone a repository)

The official https://github.com/actions/checkout action clones the repository to `$GITHUB_WORKSPACE`. By default it uses built-in `GITHUB_TOKEN` for authentication.

In most cases, this is what you need:

```yaml
- uses: actions/checkout@v4
```

The checkout action also supports pushing a commit to the same repo.

!!! warning

    This may *not* work on protected branches that need status checks.

```yaml
on: push
jobs:
  git-push:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: |
          date > generated.txt
          git config user.name github-actions
          git config user.email github-actions@github.com
          git add .
          git commit -m "generated"
          git push
```

However, no further workflows will be triggered with the [`GITHUB_TOKEN`](https://docs.github.com/en/actions/security-guides/automatic-token-authentication). You will need the following steps to trigger workflows.

### How to trigger further CI runs

You will need either a [Personal access token (PAT)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) with `repo` scope access as an [action secret](https://docs.github.com/en/actions/security-guides/encrypted-secrets).

```yaml
- uses: actions/checkout@v4
  with:
	token: ${{ secrets.PAT }}
```

Or a pair of SSH keys; the public key is the [deploy key](https://docs.github.com/en/developers/overview/managing-deploy-keys) with write access, while the private key is an action secret variable `SSH_PRIVATE_KEY`.

```yaml
- uses: actions/checkout@v4
  with:
	ssh-key: ${{ secrets.SSH_PRIVATE_KEY }}
```

## Push changes back to GitHub

The following actions are more convenient for commit and push than the official [checkout](https://github.com/actions/checkout) action.

- https://github.com/EndBug/add-and-commit
- https://github.com/stefanzweifel/git-auto-commit-action
- https://github.com/ad-m/github-push-action

## Create a pull request

The https://github.com/peter-evans/create-pull-request action will commit all files into a new branch and make a pull request to the target (default `main`) branch.

```yaml
- name: Create Pull Request
  uses: peter-evans/create-pull-request@v6
  with:
  # token: ${{ secrets.PAT }} # A PAT is required for triggering pull request workflows
    token: ${{ secrets.GITHUB_TOKEN }}  # This will not trigger further workflows
```

## Merge pull requests

+ [Kodiak Bot](https://kodiakhq.com/) : automatic merge PRs based on the issue label. (by default `automerge`). See also [auto-deps-update](./auto-deps-update.md).
+ Run `gh pr merge --merge --auto $PR_NUMBER` in the workflow.
+ https://github.com/peter-evans/enable-pull-request-automerge : A GitHub action to enable auto-merge on a pull request.
