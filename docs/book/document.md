---
title: Document processing
tags:
- bookmark
- latex
- markdown
---

## Markdown

- A curated list of [😎 awesome Markdown](https://github.com/mundimark/awesome-markdown)

<!-- more -->

### Markdown flavors

- [Commonmark](https://commonmark.org/help/)
- [Markdown-it](https://markdown-it.github.io/)
- [GitHub markdown](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [GitLab markdown](https://docs.gitlab.com/ee/user/markdown.html)
- [Pandoc markdown](https://pandoc.org/MANUAL.html#pandocs-markdown)
- [MyST (Markedly Structured Text)](https://jupyterbook.org/content/myst.html) : extended markdown syntax for [jupyter book](https://jupyterbook.org/)

### (Local) Markdown Editors

- [Markdown preview enhanced](https://shd101wyy.github.io/markdown-preview-enhanced/) VS Code plugin.
- https://github.com/marktext/marktext : Simple and Elegant Markdown Editor.
- [Zettlr](https://www.zettlr.com/) : A Markdown Editor and organizer.
- [Obsidian](https://obsidian.md/) : A markdown note writing APP.
- [memos](https://usememos.com/) : A privacy-first, lightweight note-taking service.

### Online Markdown Editors

- [Editor.md](https://pandao.github.io/editor.md/en.html)
- [HackMD](https://hackmd.io/) : Collaborative Markdown Knowledge Base.
- [Tables Generator](https://www.tablesgenerator.com/) : LaTeX and MD Tables.
- [Upmath](https://upmath.me/) : Create web articles and blog posts with equations and diagrams.

### Markdown formatters and linters

- [markdownlint](https://github.com/DavidAnson/markdownlint) : A Node.js style checker and lint tool for Markdown/CommonMark files.
- [mdformat](https://github.com/executablebooks/mdformat) : CommonMark compliant Markdown formatter.
- [markdown-formatter](https://marketplace.visualstudio.com/items?itemName=mervin.markdown-formatter) VS code plugin.

### Checking URL links

- https://github.com/scivision/linkchecker-markdown : a blazing-fast markdown link checker in *Python*.
- https://github.com/tcort/markdown-link-check : a Node.js application to check Markdown links. GitHub actions: https://github.com/marketplace/actions/markdown-link-check.
- https://github.com/lycheeverse/lychee : a fast link checker written in Rust. GitHub action: https://github.com/lycheeverse/lychee-action.

## LaTeX

- [😎 Awesome LaTeX](https://github.com/egeerardyn/awesome-LaTeX).
- [LaTeX tutorials](https://www.latex-tutorial.com/)
- [LaTeX templates](http://www.latextemplates.com/)
- [Scientific paper tips and tricks](https://github.com/Wookai/paper-tips-and-tricks) : how to write scientific papers in LaTeX, with figures generated in Python or Matlab.

### LaTeX Distributions

- [TexLive](https://tug.org/texlive/) : de-facto standard TeX distribution.
- [MiKTeX](https://miktex.org/) : A just enough TeX distribution.
- [TinyTeX](https://yihui.org/tinytex/) : for R markdown publication.
- [Tectonic](https://tectonic-typesetting.github.io/) : A modernized, complete, self-contained TeX/LaTeX engine.

### TeX Editors

- [Overleaf](https://overleaf.com) : An online LaTeX project and document manager.
- [LaTeX workshop for VS code](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop)
- [TexLab for VS Code](https://marketplace.visualstudio.com/items?itemName=efoerster.texlab) : rich editing support for the LaTeX typesetting system powered by the TexLab language server
- [Lyx](https://www.lyx.org/) : A What You See Is What You Mean document processor.
- [TEXMAKER](https://www.xm1math.net/texmaker/) : A free cross-platform LaTeX editor.
- [SwiftLaTeX](https://github.com/SwiftLaTeX/SwiftLaTeX) : SwiftLaTeX is a WYSIWYG Browser-based LaTeX Editor, based on the [Tectonic][] engine.
- [TexWorks](https://www.tug.org/texworks/) : Lowering the entry barrier to the TeX world.

### LaTeX Online Tools

- [Detexify](http://detexify.kirelabs.org/classify.html) : recognition of handwriting to Latex symbols.
- [Tables Generator](https://www.tablesgenerator.com/) : LATEX and MD Tables.
- [LaTeX live (在线LaTeX公式编辑器)](https://www.latexlive.com/) : LaTeX equations to SVG using MathJax.

### CI/CD for building LaTeX documents

[GitHub actions](https://github.com/features/actions) for automatically compile LaTeX documents on pushing changes.

- [LaTex compile gitlab template](https://gitlab.com/jasonrwang/dissertation-tudelft-latex) compiles and push result pdf files back to the repository.
- [Report Tex github template](https://github.com/stevengogogo/ReportTex)
- [Pandoc LaTeX template](https://github.com/Wandmalfarbe/pandoc-latex-template)
- [NTU Thesis CI](https://github.com/Hsins/NTU-Thesis-CI) : An automated NTU Thesis LaTeX continuous integration and continuous deploying service built up with GitHub Actions.
- Texlive: [LaTeX action](https://github.com/xu-cheng/latex-action) for a full environment and [setup-tinytex action](https://github.com/r-lib/actions/tree/v2-branch/setup-tinytex) for a minimal texLive environment.
- Tectonic: [Setup tectonic](https://github.com/WtfJoke/setup-tectonic) and the [tectonic docker image](https://github.com/WtfJoke/tectonic-docker).
