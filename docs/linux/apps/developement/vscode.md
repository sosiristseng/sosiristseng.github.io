---
title: VSCode
tags:
  - linux
---

[Visual Studio Code](https://code.visualstudio.com) is a lightweight but powerful source code editor which runs on your desktop and is available for Linux, macOS and Windows.

See also https://github.com/viatsko/awesome-vscode for a curated list of delightful VS Code packages and resources.

## Install

=== "Ubuntu"

    ```sh
    curl -fsSL https://packages.microsoft.com/keys/microsoft.asc | sudo gpg --dearmor -o /usr/share/keyrings/packages.microsoft.gpg
    echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" | sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null
    sudo apt update && sudo apt install -y code
    ```

=== "snap"

    ```sh
    sudo snap install code --classic
    ```

## VSCode Settings

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

### Markdown settings

[Markdown in VSCode](https://code.visualstudio.com/docs/languages/markdown)

+ Link validation: set `"markdown.validate.enabled": true`.
+ Automatic link updates: set `"markdown.updateLinksOnFileMove.enabled": prompt`

## VSCode extensions

- [Luna paint](https://marketplace.visualstudio.com/items?itemName=Tyriar.luna-paint): A raster image editor extension for VSCode.
- [TeXLab](https://marketplace.visualstudio.com/items?itemName=efoerster.texlab): An implementation of the Language Server Protocol for LaTeX.
- [Live server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)
- [Live Share](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare)
- [Draw.io Integration](https://marketplace.visualstudio.com/items?itemName=hediet.vscode-drawio)
- [Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack): Develop in WSL, remote SSH, etc.

### Themes

[VSCode themes](https://vscodethemes.com/)

- [Atom One Dark Theme](https://marketplace.visualstudio.com/items?itemName=akamud.vscode-theme-onedark)
- [Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)

### Version control and continuous integration (CI)

- [Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph): View a Git Graph of your repository, and perform Git actions from the graph.
- [GitHub Pull Requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github): Pull Request and Issue Provider for GitHub.
- [GitHub actions](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-github-actions)

### Formatting

- [Editor config for VS code](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig): generate [editor config](https://editorconfig.org/) files in VSCode.
- [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)
- [Even Better TOML](https://marketplace.visualstudio.com/items?itemName=tamasfe.even-better-toml)
- [YAML](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml)
- [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)

### View files

- [MPEG4 preview](https://marketplace.visualstudio.com/items?itemName=analytic-signal.preview-mp4): Simple preview for MPEG-4 (`.mp4`) video files in VSCode.
- [GitHub Markdown Preview](https://marketplace.visualstudio.com/items?itemName=bierner.github-markdown-preview): GitHub-flavored Markdown for VSCode.
- [vscode-pdf](https://marketplace.visualstudio.com/items?itemName=tomoki1207.pdf): PDF (`.pdf`) documents.
- [Rainbow CSV](https://marketplace.visualstudio.com/items?itemName=mechatroner.rainbow-csv)
- [TIFF Preview](https://marketplace.visualstudio.com/items?itemName=analytic-signal.preview-tiff): TIFF (`.tif`) images.
