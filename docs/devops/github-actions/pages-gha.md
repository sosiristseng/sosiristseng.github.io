---
title: GitHub Pages GitHub actions
tags:
  - github
  - devops
---

Publish your website to [GitHub pages](https://pages.github.com/) with GitHub actions (CI/CD).

## Official workflow

[Official GitHub actions](https://github.blog/changelog/2022-07-27-github-pages-custom-github-actions-workflows-beta/)

+ https://github.com/actions/upload-pages-artifact
+ https://github.com/actions/deploy-pages

The benefit of using the official worflow is that you do not need an orphan branch to hold the webpages.

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

In the repository settings => Pages => Build and deployment => Select `GitHub actions` as the page source.

## Publish to another branch

You need to give write permission to `GITHUB_TOKEN` in the workflow file for the following actions to work

```yaml
permissions:
  contents: write
```

Use https://github.com/peaceiris/actions-gh-pages

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

Or https://github.com/JamesIves/github-pages-deploy-action

```yaml
# After the webstie was built
- name: Deploy 🚀
  uses: JamesIves/github-pages-deploy-action@v4
  with:
    folder: ./public # The folder the action should deploy.
```

In the repository settings => Pages => Build and deployment => Select `Deploy from a branch` as the page source.
