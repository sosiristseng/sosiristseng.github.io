---
title: zotero
tags:
  - research
  - document
  - linux
  - windows
---

[Zotero](https://www.zotero.org/) is an open source reference manager.

## Install

### Ubuntu

https://github.com/retorquere/zotero-deb provides packaged versions of Zotero reference manager and Juris-M for Debian-based systems.

```sh
curl -sL https://raw.githubusercontent.com/retorquere/zotero-deb/master/install.sh | sudo bash
sudo apt update && sudo apt install -y zotero
```

### Windows

chocolatey:

```powershell
choco install zotero
```

winget:

```powershell
winget install --id=DigitalScholar.Zotero -e
```

## Zotfile attachment manager

Storage space for attachments is [limited to **300MB**](https://www.zotero.org/storage) in the free plan of Zotero. The https://github.com/jlegewie/zotfile attachment manager work around this by storing attachments to a custom folder. (e.g. Dropbox / OneDrive / Google drive folders)

- Download the `.xpi` file from ZotFile and install it via the Zotero extension interface. Restart Zotero.
- In the zotero main program preference
    - Sync -> settings -> untick `Sync attachments in my library`
    - Advanced -> Set `Linked attachment base directory` to your library folder.
- In the ZotFile settings
    - Set Location of Files to `Custom Location` and point it to your library folder.
    - (Optionally) Set `Source folder` to your download folder.

## Zotero and Obsidian collaboration

Source: [Mariana Montes' post](https://www.marianamontes.me/post/obsidian-and-zotero/)

### In the Zotero APP

- Install [Better BibTex add-on](https://github.com/retorquere/zotero-better-bibtex/releases/).\
- Define a citation key template in Zotero Preferences => Better BibTeX

![image](https://user-images.githubusercontent.com/40054455/205590043-63c0a5bb-d0f5-45db-b1fc-953e599bb971.png)

- Export your reference by right-clicking Your library => Export library => Choose `Better BibLaTeX` as the format and tick `Keep updated`. Save the library file.

### In the Obsidian APP

Assuming [Obsidian](https://obsidian.md/) has been installed.
- Install [obsidian-citation-plugin](https://github.com/hans/obsidian-citation-plugin) via the Obsidian settings => Community plugins => Browse for `Citations`.
- In the Obsidian settings => Community plugins => Citations, choose the exported BibLaTeX library file as the citation database path

![image](https://user-images.githubusercontent.com/40054455/205593774-40946d57-53ce-410e-b3f1-45843698dd6c.png)

- You can now use `Ctrl + Shift + O` to create a literature note and `Ctrl + Shift + E` to insert a link to a literature note.
