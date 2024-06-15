---
title: Setup Hugo in GitHub actions
tags:
  - github
  - hugo
  - devops
---

Use https://github.com/peaceiris/actions-hugo

```yaml
name: Deploy Hugo site to Pages

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
  workflow_dispatch:

# Allow one concurrent deployment
concurrency:
  group: pages-${{ github.ref }}
  cancel-in-progress: true

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    steps:
      - name: checkout
        uses: actions/checkout@v4
        with:
          submodules: true # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0 # Fetch all history for .GitInfo and .Lastmod
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          extended: true
      - name: Caching Hugo Modules
        uses: actions/cache@v4
        with:
          path: ~/.cache/hugo_cache
          key: ${{ runner.os }}-hugomod-${{ hashFiles('**/go.sum') }}
          restore-keys: |
            ${{ runner.os }}-hugomod-
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v3
      - name: Build
        run: hugo --gc --minify --baseURL ${{ steps.pages.outputs.base_url }}
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: ./public

  # Deployment job
  deploy:
    needs: build
    if: github.ref == 'refs/heads/main'
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
