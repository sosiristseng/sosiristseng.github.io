---
title: Git Operations in GitHub actions
draft: false
tags:
  - git
  - github
  - devops
---
Git commands, such as checkout, add, make a branch/pull request in Github actions.
## Checkout

The official <https://github.com/actions/checkout> action clones the repository to `$GITHUB_WORKSPACE`. By defualt it uses built-in `GITHUB_TOKEN` for authentication.

In most cases, this is what you need:

```yaml
- uses: actions/checkout@v3
```

The checkout action also supports pushing a commit to the same repo.

> [!warning]
> This may *not* work on protected branches that need status checks.

```yaml
on: push
jobs:
  git-push:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: |
          date > generated.txt
          git config user.name github-actions
          git config user.email github-actions@github.com
          git add .
          git commit -m "generated"
          git push
```

However, no further workflows will be triggered with the [`GITHUB_TOKEN`](https://docs.github.com/en/actions/security-guides/automatic-token-authentication). You will need the following steps to trigger workflows.

### How to trigger CI runs

You will need either a [Personal access token (PAT)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) with `repo` scope access as an [action secret](https://docs.github.com/en/actions/security-guides/encrypted-secrets).

```yaml
- uses: actions/checkout@v3
  with:
	toekn: ${{ secrets.PAT }}
```

Or a pair of SSH keys; the public key is the [deploy key](https://docs.github.com/en/developers/overview/managing-deploy-keys) with write access, while the private key is an action secret variable `SSH_PRIVATE_KEY`.

```yaml
- uses: actions/checkout@v3
  with:
	ssh-key: ${{ secrets.SSH_PRIVATE_KEY }}
```

## Pushing changes back to GitHub

The following actions are more convenient for commit and push than the official [checkout](https://github.com/actions/checkout) action.

- <https://github.com/EndBug/add-and-commit>
- <https://github.com/stefanzweifel/git-auto-commit-action>
- <https://github.com/ad-m/github-push-action>
## Create pull request

The <https://github.com/peter-evans/create-pull-request> action will commit all files into a new branch and make a pull request to the target (default `main`) branch.

```yaml
- name: Create Pull Request
  uses: peter-evans/create-pull-request@v3
  with:
  # token: ${{ secrets.PAT }} # A PAT is required for triggering pull request workflows
    token: ${{ secrets.GITHUB_TOEKN }}  # This will not trigger further workflows
```

## Merge pull requests

- [Kodiak Bot](https://kodiakhq.com/) : automatic merge PRs based on the issue label. (by default `automerge`). See also [[auto-deps-update]].

## Publish to GitHub pages

### Official workflow

[Official GitHub actions](https://github.blog/changelog/2022-07-27-github-pages-custom-github-actions-workflows-beta/)

- <https://github.com/actions/upload-pages-artifact>
- <https://github.com/actions/deploy-pages>

The benefit of using the official worflow is that you do not need another branch to hold the webpages.

```yaml title=".github/workflows/pages.yml"
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      # After the website is built
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v1
        if: ${{ github.ref == 'refs/heads/main' }}
        with:
          path: ./site

  # Deployment job
  deploy:
    needs: build
    if: ${{ github.ref == 'refs/heads/main' }}
    # Grant GITHUB_TOKEN the permissions required to make a Pages deployment
    permissions:
      pages: write # to deploy to Pages
      id-token: write # to verify the deployment originates from an appropriate source
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```

### Publish to another branch

Use <https://github.com/peaceiris/actions-gh-pages>

```yaml
# After the webstie was built
- name: Deploy
  uses: peaceiris/actions-gh-pages@v3
  with:
    github_token: ${{ secrets.GITHUB_TOKEN }}  # You need an SSH deploy key if deploying to another repo
    publish_dir: ./public
    force_orphan: true
    commit_message: ${{ github.event.head_commit.message }}
```

Or <https://github.com/JamesIves/github-pages-deploy-action>

```yaml
# After the webstie was built
- name: Deploy 🚀
  uses: JamesIves/github-pages-deploy-action@v4
  with:
    branch: gh-pages # The branch the action should deploy to.
    folder: ./public # The folder the action should deploy.
```

## Synchronize Git repo

The [git-sync](https://github.com/wei/git-sync) action synchonizes one repository to another.

```yaml title=".github/workflows/git-sync.yml"
on: push
jobs:
  git-sync:
    runs-on: ubuntu-latest
    steps:
      - name: git-sync
        uses: wei/git-sync@v3
        with:
          source_repo: "source_org/repository" # Default to GitHub
          source_branch: "main"
          destination_repo: "git@gitlab.com:username/repository.git" # Use SSH URL for other Git providers
          destination_branch: "main"
          ssh_private_key: ${{ secrets.SSH_PRIVATE_KEY }} # optional
          source_ssh_private_key: ${{ secrets.SOURCE_SSH_PRIVATE_KEY }} # optional, will override `SSH_PRIVATE_KEY`
          destination_ssh_private_key: ${{ secrets.DESTINATION_SSH_PRIVATE_KEY }} # optional, will override `SSH_PRIVATE_KEY`
```

You need a pair of SSH keys. The public key becomes the [deploy key](https://docs.github.com/en/developers/overview/managing-deploy-keys) with write access, while the private key cecomes an action secret variable `SSH_PRIVATE_KEY`.
