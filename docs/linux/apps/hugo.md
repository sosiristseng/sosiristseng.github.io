---
title: Hugo
tags:
  - web
  - linux
  - github
  - devops
  - static-site-generator
---

[Hugo](https://gohugo.io/) is the world’s fastest framework for building websites, written in Go.

## Install Hugo

=== "Ubuntu"

    Download and install the hugo `deb` file from the [release page](https://github.com/gohugoio/hugo/releases/latest).

## Hugo in GitHub actions

[Hugo in GitHub actions](../code/github-actions/runtime/hugo-gha.md)

## Hugo in docker

[klakegg/hugo](https://hub.docker.com/r/klakegg/hugo/)

```dockerfile
FROM klakegg/hugo
```

## Hugo themes

A list of **[Hugo themes](https://themes.gohugo.io/)** I found useful

### Documentation

- https://github.com/vantagedesign/ace-documentation
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
