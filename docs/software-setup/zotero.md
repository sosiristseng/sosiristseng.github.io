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

Download and install [Zotero](https://www.zotero.org/) from the official website or

=== "Ubuntu"

    https://github.com/retorquere/zotero-deb provides packaged versions of Zotero reference manager and Juris-M for Debian-based systems.

    ```sh
    curl -sL https://raw.githubusercontent.com/retorquere/zotero-deb/master/install.sh | sudo bash
    sudo apt update && sudo apt install -y zotero
    ```

=== "Windows"

    chocolatey:

    ```powershell
    choco install zotero
    ```

    winget:

    ```powershell
    winget install DigitalScholar.Zotero
    ```

## Attachment files management

In the Zotero free plan, the storage space for attachments is [limited to **300MB**](https://www.zotero.org/storage).

### Use WebDAV

Free online storage spaces supporting the WebDAV protocol.

- [koofr](https://koofr.eu/) (Slovenia(EU)-based): 10GB free. See [Koofr with Zotero via WebDAV](https://koofr.eu/blog/posts/koofr-with-zotero-via-webdav) for details.
- [Infinicloud](https://infini-cloud.net/en/index.html) (Japan-based): 20 GB free. See [connecting Zotero and infinicloud](https://infini-cloud.net/en/clients_zotero.html)

In Zotero settings
- Sync => File Syncing, enable sync attachment files in My Library and choose WebDAV. Follow the instructions from the service provider to setup and login their service.

### Move attachments by ZotMoov plugin

You can setup a folder synchronized with online services (OneDrive, Google Drive, DropBox, and Koofr, etc) and use ZotMoov to automatically move Zotero attachments into that folder.

Assuming that folder is `D:\obsidian\pdf` (Yes, I put it inside my obsidian vault)

In Zotero settings
- Sync => File Syncing, disable sync attachment files in My Library.
- Advanced => Files and Folders => Linked attachment base directory => Choose `D:\obsidian\pdf`.
- Zotmoov => Directory to Move/Copy files to => Choose `D:\obsidian\pdf`.


## Zotero plugins

https://www.zotero.org/support/plugins

- [Better BibTex](https://retorque.re/zotero-better-bibtex/) : auto generates stable citation keys without clashes.
- [Better Notes](https://github.com/windingwind/zotero-better-notes): note taking, annotating, exporting, and synchronization. (Optional, as I use Obsidian to take notes)
- [ZotMoov](https://github.com/wileyyugioh/zotmoov): a _simple_ plugin for managing attachments in Zotero 7. It provides workaround for space limitations (300MB) of online attachment.


## Zotero and Obsidian collaboration

Source: [Mariana Montes' post](https://www.marianamontes.me/post/obsidian-and-zotero/)

### Zotero side

- Install [Better BibTex](https://github.com/retorquere/zotero-better-bibtex/releases/) plugin.
- Define a citation key template in Zotero Preferences => Better BibTeX

![](https://github.com/user-attachments/assets/1ef648ac-599f-4f67-b1af-42c41244b57d)

### Obsidian side

- Install [Obsidian](https://obsidian.md/)
- Install [Zotero integration](https://github.com/mgmeyers/obsidian-zotero-integration) plugin
- Setup a Obsidian template for literature notes. I save the following text to `_templates/Zotero integration template.md`.

```markdown title="Zotero integration template.md"
---
year: '{{date | format("YYYY")}}'
tags:
citekey: "{{citekey}}"
authors: "{{authors}}"
DOI: "{{DOI}}"
url: "{{url}}"
Zotero link: "{{desktopURI}}"
Journal: "{{journalAbbreviation}}"
Created: 2025-08-10, 15:34:47
Modified: 2025-10-04, 20:48:00
---

# {{title | escape}}

> [!Abstract]-
> {% if abstractNote %}
> {{abstractNote}}
> {% endif %}

> [!Cite]-
> {{bibliography}}

> [!note] PDF link
> {{pdfZoteroLink}}

## Persistent Notes

{% persist "notes" %}{% if isFirstImport %}
`Write your note here.`
{% endif %}{% endpersist %}

## In-text annotations

{% for annotation in annotations -%}
{%- if annotation.annotatedText -%}
{{annotation.annotatedText | safe}}
{%- endif -%}
{% if annotation.comment %}
{{annotation.comment | safe}}
{% endif %}

>  [Page {{annotation.pageLabel}}](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.pageLabel}}&annotation={{annotation.id}})

{% if annotation.imageRelativePath %}
![[{{annotation.imageRelativePath}}]]{% endif %}
{% endfor -%}

```

- In the obsidian settings => Zotero integration, setup import formats as follows

![](https://github.com/user-attachments/assets/deaaf325-3333-443e-9c01-6bc4aa924269)


And you can use `Ctrl+P` commands => Zotero integration: Literature note to import paper information into obsidian vault.
