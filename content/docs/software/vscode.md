---
title: vscode
tags:
  - development
---

[Visual Studio Code](https://code.visualstudio.com) is a lightweight but powerful source code editor which runs on your desktop and is available for Linux, macOS and Windows.

<!--more-->

## Install

### Ubuntu (deb)

```sh
curl -fsSL https://packages.microsoft.com/keys/microsoft.asc | sudo gpg --dearmor -o /usr/share/keyrings/packages.microsoft.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" | sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null
sudo apt update && sudo apt install -y code
```

### Ubuntu (snap)

```sh
sudo snap install code --classic
```

### Windows

chocolatey:

```powershell
choco install vscode
```

winget:

```powershell
winget install Microsoft.VisualStudioCode
```

## VSCode Settings

To open the settings file (`settings.json`):
`Ctrl` + `Shift` + `P` => Preferences: Open user settings (JSON)

### Change VS Code UI font

1. Install the [Customize UI](https://marketplace.visualstudio.com/items?itemName=iocave.customize-ui) plugin and restart VS Code.[^1]
2. In VS Code Settings, set `Customize UI Font:Monospace` and/or `Customize UI Font:Regular` to your liking.

[^1]: https://stackoverflow.com/questions/57008558/how-to-change-the-font-of-visual-studio-codes-ui

### Better-looking menu bar

Add this entry to `settings.json` ([Ask Ubuntu thread](https://askubuntu.com/questions/1197231/visual-studio-code-ui-is-visually-mismatched-in-ubuntu-19-1))

```json
{
  "window.titleBarStyle": "custom",
}
```

Reload VSCode to apply the changes.

### Line height

You can increase line height to make you code look better.

Search for `Line height` in VSCode settings and set it to a higher number. (For example, 1.4)

```json
{
  "editor.lineHeight": 1.4,
}
```

### Markdown settings

[Markdown in VSCode](https://code.visualstudio.com/docs/languages/markdown)

Link validation + Automatic link updates
```json
{
  "markdown.validate.enabled": true,
  "markdown.updateLinksOnFileMove.enabled": prompt
}
```

## VSCode extensions

- [Foam](https://marketplace.visualstudio.com/items?itemName=foam.foam-vscode): Foam is a note-taking tool that lives within VS Code, similar to [Obsidian](https://obsidian.md/).
- [Live server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)
- [Live Share](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare)
- [Luna paint](https://marketplace.visualstudio.com/items?itemName=Tyriar.luna-paint): A raster image editor extension for VSCode.
- [Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack): Develop in WSL, remote SSH, etc.

### Themes

[VSCode themes](https://vscodethemes.com/)

- [Atom One Dark Theme](https://marketplace.visualstudio.com/items?itemName=akamud.vscode-theme-onedark)
- [One Dark Pro Theme](https://marketplace.visualstudio.com/items?itemName=zhuangtongfa.Material-theme)
- [Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)

### Version control and continuous integration (CI)

- [Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph): View a Git Graph of your repository, and perform Git actions from the graph.
- [GitHub Pull Requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github): Pull Request and Issue Provider for GitHub.
- [GitHub actions](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-github-actions)

### Formatting

- [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)
- [Editor config for VS code](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig): generate [editor config](https://editorconfig.org/) files in VSCode.

### Documents

- [Draw.io](https://marketplace.visualstudio.com/items?itemName=hediet.vscode-drawio) : This unofficial extension integrates Draw.io diagrams into VS Code.

Markdown:

- [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)
- [Markdown table](https://marketplace.visualstudio.com/items?itemName=TakumiI.markdowntable)
- [GitHub Markdown Preview](https://marketplace.visualstudio.com/items?itemName=bierner.github-markdown-preview): GitHub-flavored Markdown for VSCode.

LeTeX:

- [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) : LaTeX typesetting.
- [TeXLab](https://marketplace.visualstudio.com/items?itemName=efoerster.texlab): An implementation of the Language Server Protocol for LaTeX.

Typst:

- [Tinymist Typst](https://marketplace.visualstudio.com/items?itemName=myriad-dreamin.tinymist): Typst documents support.

### View files

- [MATLAB](https://marketplace.visualstudio.com/items?itemName=MathWorks.language-matlab): matlab(`.m`) files.
- [MPEG4 preview](https://marketplace.visualstudio.com/items?itemName=analytic-signal.preview-mp4): Simple preview for MPEG-4 (`.mp4`) video files in VSCode.
- [Rainbow CSV](https://marketplace.visualstudio.com/items?itemName=mechatroner.rainbow-csv): CSV (`.csv`) files.
- [TIFF Preview](https://marketplace.visualstudio.com/items?itemName=analytic-signal.preview-tiff): TIFF (`.tif`) images.
- [vscode-pdf](https://marketplace.visualstudio.com/items?itemName=tomoki1207.pdf): PDF (`.pdf`) documents.
- [YAML](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml) : YAML `.yml` files.
- [Even Better TOML](https://marketplace.visualstudio.com/items?itemName=tamasfe.even-better-toml) : TOML `.toml` files.
