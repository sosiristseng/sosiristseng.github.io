---
title: zotero
tags:
  - research
  - document
---

[Zotero](https://www.zotero.org/) is an open source reference manager.

- [Zotero Chinese community](https://zotero-chinese.com/)

<!--more-->

## Install

Download and install [Zotero](https://www.zotero.org/) from the official website or

**Ubuntu**

[zotero-deb](https://github.com/retorquere/zotero-deb) provides packaged versions of Zotero reference manager and Juris-M for Debian-based systems.

```sh
curl -sL https://raw.githubusercontent.com/retorquere/zotero-deb/master/install.sh | sudo bash
sudo apt update && sudo apt install -y zotero
```

**Windows**

chocolatey:

```powershell
choco install zotero
```

winget:

```powershell
winget install DigitalScholar.Zotero
```

## Zotero plugins

https://www.zotero.org/support/plugins

- [Actions and Tags for Zotero][atz] : Automates your workflow with tags and custom scripts
- [Better BibTex](https://retorque.re/zotero-better-bibtex/) : auto generates stable citation keys without clashes.
- [Better Notes](https://github.com/windingwind/zotero-better-notes): note taking, annotating, exporting, and synchronization. (Optional, as I use Obsidian to take notes)
- [ZotMoov](https://github.com/wileyyugioh/zotmoov): a simple plugin for managing attachments in Zotero 7. It provides workaround for space limitations (300MB) of online attachment.

[atz]: https://github.com/windingwind/zotero-actions-tags "Actions and Tags for Zotero"

## Synchronize attachments across devices

In the Zotero free plan, the storage space for attachments is [limited to **300MB**](https://www.zotero.org/storage).

### Use WebDAV

Free online storage spaces supporting the WebDAV protocol.

- [koofr](https://koofr.eu/) (Slovenia(EU)-based): 10GB free. See [Koofr with Zotero via WebDAV](https://koofr.eu/blog/posts/koofr-with-zotero-via-webdav) for details.
- [Infinicloud](https://infini-cloud.net/en/index.html) (Japan-based): 20 GB free. See [connecting Zotero and infinicloud](https://infini-cloud.net/en/clients_zotero.html)

In Zotero settings: `Sync` => `File Syncing`, enable sync attachment files in My Library and choose WebDAV. Follow the instructions from the service provider to setup and login their service. For the Koofr example,

![Zotero WebDav Koofr](https://github.com/user-attachments/assets/317dc7a0-d588-4ed2-bbd8-eb05feb7913f)

### Use ZotMoov

You can setup a folder synchronized with online services (OneDrive, Google Drive, DropBox, and Koofr, etc) and use ZotMoov to automatically move Zotero attachments into that folder.

Assuming that synchronized folder is `D:\pdf`

In Zotero settings

- `Sync` => File Syncing, disable sync attachment files in My Library.
- `Advanced` => Files and Folders => Linked attachment base directory => Choose `D:\pdf`.
- `Zotmoov` => Directory to Move/Copy files to => Choose `D:\pdf`.

## Tweaks

### Disable automatic tag generation

Zotero settings -> General -> Misc -> Uncheck "Automatically tag items with keywords and subject headings" .

### Citation key customization

You can customize the citation key creation by editing `Better BibTeX` -> `Citation keys`. For instance,

```
auth.lower + year
```

## Zotero and Obsidian collaboration

See the [Zotlit](https://github.com/aidenlx/zotlit) Obsidian plugin.

## Copy Zotero item link

To copy a direct Zotero item link (`zotero://select/...`),

1. Install the  [Actions and Tags for Zotero][atz] plugin.
2. Open Zotero Settings / Preferences -> Actions & Tags
3. Click the + button to create a new action:
	• Operation: Select customScript.
	• Menu label: Copy item link.
	• Shortcut: Assign a custom keyboard shortcut (e.g., Ctrl+Shift+C or Cmd+Shift+C).
	• Data field: Paste the community copy-link script from the Actions & Tags [GitHub Discussion](https://github.com/windingwind/zotero-actions-tags/discussions/115) (displayed below)
4. Right-click any item in your library and select Copy item link from the menu or press your shortcut to copy zotero://select/library/items/[ITEM_KEY] to your clipboard
