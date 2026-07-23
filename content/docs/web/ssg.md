---
title: Static site generators
tags:
  - web
---

- [Awesome static site generators](https://github.com/myles/awesome-static-generators)

## Pandoc-based

- [Quarto](https://quarto.org/): an open-source scientific and technical publishing system built on **Pandoc**.

## R-based

- [Bookdown](https://bookdown.org) : Write HTML, PDF, ePub, and Kindle books with R Markdown. Written in `R`.

## Ruby-based

- [Jekyll](https://jekyllrb.com) : The default SSG for GitHub pages. Written in `Ruby`.
	- [Just the docs template](https://just-the-docs.github.io/just-the-docs-template/)
	- [chirpy template](https://github.com/sosiristseng/template-jekyll-chirpy)

## Rust-based

- [mdBook](https://github.com/rust-lang/mdBook) : Create book from markdown files. Like Gitbook but written in `Rust`. See also [GitHub actions for mdbook](https://github.com/peaceiris/actions-mdbook).
- [zola](https://github.com/getzola/zola) : A fast static site generator in a single Rust binary with everything built-in. See also the [GitHub actions for Zola](https://github.com/TonySpegel/zola-build-action).

## Python-based

- [Jupyter book](https://jupyterbook.org/) : Building beautiful, publication-quality books and documents from jupyter notebooks.
- [Nikola](https://getnikola.com/) : Static Site Generator written in Python.

## Julia-based

- [Franklin.jl](https://github.com/tlienart/Franklin.jl) : Static site generation with live Julia code evaluation. [Examples](https://github.com/tlienart/Franklin.jl#docs).
- [PkgPage.jl](https://github.com/JuliaDocs/PkgPage.jl) : Creating (package) front-pages, powered by `Franklin.jl`.
- [StaticWebPages.jl](https://github.com/Azzaare/StaticWebPages.jl) : Create academics and personal CV web-pages.
- [PlutoStaticHTML.jl](https://github.com/rikhuijzer/PlutoStaticHTML.jl) : Convert Pluto notebooks to pure HTML files

## JS-based

- [11ty](https://www.11ty.dev/) : a simple SSG written in JavaScript.
- [Publii](https://github.com/GetPublii/Publii) : A content management system (CMS) for creating static websites fast and hassle-free, even for beginners.

### Docsify

[Docsify](https://docsify.js.org/) renders Markdown files to HTML on-the-fly. Technically docsify is a single page application (SPA) rather than a static site generator (SSG).

- [docsify-open-publishing-starter-kit](https://github.com/hibbitts-design/docsify-open-publishing-starter-kit)
- [docsify-js-tutorial](https://github.com/MichaelCurrin/docsify-js-tutorial)
- [My docsify template](https://github.com/sosiristseng/template-docsify)

### Hexo

[Hexo](https://hexo.io/) is a fast, simple & powerful blog framework powered by `Node.js`.

A list of **[Hexo themes](https://hexo.io/themes/)**

- [Next](https://theme-next.js.org/). Template: https://github.com/sosiristseng/template-hexo-next
- [fluid](https://fluid-dev.github.io/hexo-fluid-docs/)
- [butterfly](https://butterfly.js.org/)

## Hugo

[Hugo](https://gohugo.io/) is the world’s fastest framework for building websites, written in Go.

### Setup Hugo

#### Ubuntu

Download and install the hugo `deb` file from the [release page](https://github.com/gohugoio/hugo/releases/latest).

#### Windows

chocolatey:

```powershell
choco install hugo-extended
```

Go compiler is needed for Hugo modules

```powershell
choco install golang
```

#### GitHub actions

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

#### Docker

[klakegg/hugo](https://hub.docker.com/r/klakegg/hugo/) docker image.

```dockerfile
FROM klakegg/hugo
```

### Hugo themes

A list of **[Hugo themes](https://themes.gohugo.io/)** I found useful

#### Documentation

- https://github.com/alex-shpak/hugo-book. Template: https://github.com/sosiristseng/template-hugo-book
- https://github.com/thegeeklab/hugo-geekdoc
- https://github.com/McShelby/hugo-theme-relearn. Template: https://github.com/sosiristseng/template-hugo-relearn
- https://github.com/imfing/hextra : Modern, batteries-included Hugo theme for creating beautiful doc, blog and static websites

#### Blog

- https://github.com/HEIGE-PCloud/DoIt. Template: https://github.com/sosiristseng/template-hugo-doit
- https://github.com/hugo-fixit/FixIt. Template: https://github.com/hugo-fixit/hugo-fixit-starter
- https://github.com/chipzoller/hugo-clarity
- https://github.com/adityatelange/hugo-PaperMod
- https://github.com/razonyang/hugo-theme-bootstrap
- https://github.com/CaiJimmy/hugo-theme-stack. Template: https://github.com/CaiJimmy/hugo-theme-stack-starter
- https://github.com/hugo-toha/toha
