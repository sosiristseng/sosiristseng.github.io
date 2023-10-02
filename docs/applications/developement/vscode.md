---
title: VSCode
draft: false
tags:
  - linux
  - windows
---
[Visual Studio Code](https://code.visualstudio.com) is a lightweight but powerful source code editor which runs on your desktop and is available for Linux, macOS and Windows. See also [awesome VSCode](https://github.com/viatsko/awesome-vscode).
## Install

### Ubuntu

```sh
curl -fsSL https://packages.microsoft.com/keys/microsoft.asc | sudo gpg --dearmor -o /usr/share/keyrings/packages.microsoft.gpg

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" | sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null

sudo apt update && sudo apt install -y code
```

### Arch Linux

Install from the AUR
```sh
yay -S visual-studio-code-bin
```

The open source version (sourced directly from the GitHub repo) is avaiable in the community repository.

```sh
sudo pacman -S code
```

### snap

```sh
sudo snap install code --classic
```

### Windows (chocolatey)

```powershell
choco install vscode
```

### Windows (winget)

```powershell
winget install vscode
```
## Settings

### Change VS Code UI font

1. Install the [Customize UI](https://marketplace.visualstudio.com/items?itemName=iocave.customize-ui) plugin and restart VS Code.[^1]
2. In VS Code Settings, set `Customize UI Font:Monospace` and/or `Customize UI Font:Regular` to your liking.
[^1]: https://stackoverflow.com/questions/57008558/how-to-change-the-font-of-visual-studio-codes-ui

### Use a better-looking menu bar

Add this entry to `settings.json`: [^2]

```json title=settings.json
{
  "window.titleBarStyle": "custom",
}
```

And reload VS Code.

[^2]: https://askubuntu.com/questions/1197231/visual-studio-code-ui-is-visually-mismatched-in-ubuntu-19-1

### Line height
You can increase line height to make you code look better.
Search for `Line height` in VSCode setting and set it to a higher number. (For example, 1.4)
## Interesting VS Code extensions

- [Luna paint](https://marketplace.visualstudio.com/items?itemName=Tyriar.luna-paint): A raster image editor extension for VSCode.
- [TeXLab](https://marketplace.visualstudio.com/items?itemName=efoerster.texlab): An implementation of the Language Server Protocol for LaTeX.
- [Editor config for VS code](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig): generate [editor config](https://editorconfig.org/) files in VSCode.
- [MPEG4 preview](https://marketplace.visualstudio.com/items?itemName=analytic-signal.preview-mp4): Simple preview for MPEG-4 (`.mp4`) video files in VSCode.
- [GitHub Markdown Preview](https://marketplace.visualstudio.com/items?itemName=bierner.github-markdown-preview): GitHub-flavored Markdown for VSCode.
- [vscode-pdf](https://marketplace.visualstudio.com/items?itemName=tomoki1207.pdf): Previewing for PDF (`.pdf`) files.
- [Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph): View a Git Graph of your repository, and perform Git actions from the graph.