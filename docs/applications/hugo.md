---
title: Hugo
draft: false
tags:
  - web
  - linux
  - windows
  - github
  - devops
---

[Hugo](https://gohugo.io/) is the world’s fastest framework for building websites, written in Go. 

## Installation

### Ubuntu
Download and install hugo binary from the [release page](https://github.com/gohugoio/hugo/releases/latest). Or use snap:

```powershell
sudo snap install hugo
sudo snap connect hugo:removable-media
sudo snap connect hugo:ssh-keys
```

### Arch Linux

```bash
sudo pacman -S hugo
```

### Windows

Via chocolatey:

```powershell
choco install hugo-extended
```

Go compiler is needed for install Hugo modules

```powershell
choco install golang
```

## Docker image

[klakegg/hugo](https://hub.docker.com/r/klakegg/hugo/)

```dockerfile
FROM klakegg/hugo
```
## Github actions

[Hugo Github action](https://github.com/peaceiris/actions-hugo) by peaceiris.

```yaml
name: GitHub Pages

on:
  push:
    branches:
      - main  # Set a branch to deploy
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-22.04
    concurrency:
      group: ${{ github.workflow }}-${{ github.ref }}
    steps:
      - uses: actions/checkout@v3
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          # extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref == 'refs/heads/main'
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```
## Hugo themes

A list of **[Hugo themes](https://themes.gohugo.io/)** I found useful

### Documentation

- [ace-documentation](https://github.com/vantagedesign/ace-documentation)
- [doks](https://github.com/h-enk/doks). Template: [doks-child-theme](https://github.com/h-enk/doks-child-theme)
- [hugo-book](https://github.com/alex-shpak/hugo-book)
- [hugo-geekdoc](https://github.com/thegeeklab/hugo-geekdoc)
- [hugo-theme-relearn](https://github.com/McShelby/hugo-theme-relearn)
### Blogs

- [DoIT](https://github.com/HEIGE-PCloud/DoIt)
- [hugo-clarity](https://github.com/chipzoller/hugo-clarity)
- [hugo-notepadium](https://github.com/cntrump/hugo-notepadium)
- [hugo-PaperMod](https://github.com/adityatelange/hugo-PaperMod)
- [hugo-theme-bootstrap](https://github.com/razonyang/hugo-theme-bootstrap)
- [hugo-theme-meme](https://github.com/reuixiy/hugo-theme-meme)
- [hugo-theme-stack](https://github.com/CaiJimmy/hugo-theme-stack) . Template: [hugo-theme-stack-starter](https://github.com/CaiJimmy/hugo-theme-stack-starter)
- [toha](https://github.com/hugo-toha/toha)
- [wowchemy-hugo-themes](https://github.com/wowchemy/wowchemy-hugo-themes)

### Hugo theme components

- [Hugo modules](https://hugomods.com/): Various modules for Hugo
- [hugo-notice](https://github.com/martignoni/hugo-notice) : A Hugo theme component to display nice notices.

## Github template repositories by me

- Hugo Book theme: <https://github.com/sosiristseng/template-hugo-book>
- Hugo DoIt theme: <https://github.com/sosiristseng/template-hugo-doit>
- Hugo Relearn theme: <https://github.com/sosiristseng/template-hugo-relearn>
