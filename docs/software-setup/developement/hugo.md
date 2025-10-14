---
title: hugo
tags:
  - web
  - linux
  - static-site-generator
---

[Hugo](https://gohugo.io/) is the world’s fastest framework for building websites, written in Go.

## Setup Hugo

### Ubuntu

Download and install the hugo `deb` file from the [release page](https://github.com/gohugoio/hugo/releases/latest).

### Windows

chocolatey:

```powershell
choco install hugo-extended
```

Go compiler is needed for Hugo modules

```powershell
choco install golang
```

### GitHub actions

Use https://github.com/peaceiris/actions-hugo

```yaml
name: Deploy Hugo site to Pages

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
  workflow_dispatch:

# Allow only one concurrent deployment
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

### Docker

[klakegg/hugo](https://hub.docker.com/r/klakegg/hugo/) docker image.

```dockerfile
FROM klakegg/hugo
```

## Hugo themes

A list of **[Hugo themes](https://themes.gohugo.io/)** I found useful

### Documentation

- https://github.com/gethyas/doks
- https://github.com/alex-shpak/hugo-book. Template: https://github.com/sosiristseng/template-hugo-book
- https://github.com/thegeeklab/hugo-geekdoc
- https://github.com/McShelby/hugo-theme-relearn. Template: https://github.com/sosiristseng/template-hugo-relearn

### Blogs

- https://github.com/HEIGE-PCloud/DoIt. Template: https://github.com/sosiristseng/template-hugo-doit
- https://github.com/hugo-fixit/FixIt. Template: https://github.com/hugo-fixit/hugo-fixit-starter
- https://github.com/chipzoller/hugo-clarity
- https://github.com/cntrump/hugo-notepadium
- https://github.com/adityatelange/hugo-PaperMod
- https://github.com/razonyang/hugo-theme-bootstrap
- https://github.com/reuixiy/hugo-theme-meme
- https://github.com/CaiJimmy/hugo-theme-stack. Template: https://github.com/CaiJimmy/hugo-theme-stack-starter
- https://github.com/hugo-toha/toha
- https://github.com/HugoBlox/hugo-blox-builder

### Hugo theme components

- [Hugo modules](https://hugomods.com/): Various modules for Hugo
- [hugo-notice](https://github.com/martignoni/hugo-notice) : A Hugo theme component to display nice notices.

## Hugo tips

### Parse relative links

[Forum link](https://discourse.gohugo.io/t/relative-markdown-links-markdown-render-hooks/22674)

You can use this form normally in Hugo

```markdown
[My Article](../my-article/index.md)
```

by adding the following lines to `project/layouts/_default/_markup/render-link.html`

```html
<a href="{{ (.Page.GetPage .Destination).RelPermalink | safeURL }}">{{ .Text | safeHTML }}</a>
```
