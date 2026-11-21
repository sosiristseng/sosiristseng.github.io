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

Source: [Mariana Montes' post](https://www.marianamontes.me/post/obsidian-and-zotero/)

### Zotero side

- Install [Better BibTex](https://github.com/retorquere/zotero-better-bibtex/releases/) plugin.
- Define a citation key template in Zotero Preferences => Better BibTeX

![](https://github.com/user-attachments/assets/1ef648ac-599f-4f67-b1af-42c41244b57d)

### Obsidian side

- Install [Obsidian](https://obsidian.md/)
- Install [Zotero integration](https://github.com/mgmeyers/obsidian-zotero-integration) plugin
- Setup a Obsidian template for literature notes. I save the following text to `_templates/Zotero integration template.md`.

```markdown {filename="Zotero integration template.md"}
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

The script to copy a Zotero item link:

```js
// @author windingwind, garth74
// @link https://github.com/windingwind/zotero-actions-tags/discussions/115
// @usage Select an item in the library and press the assigned shortcut keys
// @update Mon, 22 Jan 2024 00:10:18 GMT (by new Date().toGMTString())

// EDIT THESE SETTINGS

/** @type {string} Name of the field to use as the link text. To use the citation key, set this to "citationKey". */
let linkTextField = "title";

/** @type {'html' | 'md' | 'plain'} What type of link to create. */
let linkType = "html";

/** @type {boolean} If true, make the link specific to the currently selected collection. */
let useColl = false;

/** @type {boolean} If true, use Better Notes zotero://note link when the selected item is a note. */
let useNoteLink = false;

/** @type {'select' | 'open-pdf' | 'auto'} Action of link*/
let linkAction = "auto"; // auto = open-pdf for PDFs and annotations, select for everything else

// END OF EDITABLE SETTINGS

// For efficiency, only execute once for all selected items
if (item) return;
item = items[0];
if (!item && !collection) return "[Copy Zotero Link] item is empty";

if (collection) {
  linkAction = "select";
  useColl = true;
}

if (linkAction === "auto") {
  if (item.isPDFAttachment() || item.isAnnotation()) {
    linkAction = "open-pdf";
  } else {
    linkAction = "select";
  }
}

const uriParts = [];
let uriParams = "";

let targetItem = item;
if (linkAction === "open-pdf") {
  uriParts.push("zotero://open-pdf");
  if (item.isRegularItem()) {
    targetItem = (await item.getBestAttachments()).find((att) =>
      att.isPDFAttachment()
    );
  } else if (item.isAnnotation()) {
    targetItem = item.parentItem;
    // If the item is an annotation, we want to open the PDF at the page of the annotation
    let pageIndex = 1;
    try {
      pageIndex = JSON.parse(item.annotationPosition).pageIndex + 1;
    } catch (e) {
      Zotero.warn(e);
    }
    uriParams = `?page=${pageIndex}&annotation=${item.key}`;
  }
} else {
  uriParts.push("zotero://select");
  if (item?.isAnnotation()) {
    targetItem = item.parentItem;
  }
}

if (!targetItem && !collection) return "[Copy Zotero Link] item is invalid";

// Get the link text using the `link_text_field` argument
let linkText;
if (collection) {
  // When `collection` is truthy, this script was triggered in the collection menu.
  // Use collection name if this is a collection link
  linkText = collection.name;
} else if (item.isAttachment()) {
  // Try to use top-level item for link text
  linkText = Zotero.Items.getTopLevel([item])[0].getField(linkTextField);
} else if (item.isAnnotation()) {
  // Add the annotation text to the link text
  linkText = `${targetItem.getField(linkTextField)}(${
    item.annotationComment || item.annotationText || "annotation"
  })`;
} else {
  // Use the item's field
  linkText = item.getField(linkTextField);
}

// Add the library or group URI part (collection must go first)
let libraryType = (collection || item).library.libraryType;
if (libraryType === "user") {
  uriParts.push("library");
} else {
  uriParts.push(
    `groups/${Zotero.Libraries.get((collection || item).libraryID).groupID}`
  );
}

// If useColl, make the link collection specific
if (useColl) {
  // see https://forums.zotero.org/discussion/73893/zotero-select-for-collections
  let coll = collection || Zotero.getActiveZoteroPane().getSelectedCollection();

  // It's possible that a collection isn't selected. When that's the case,
  // this will fall back to the typical library behavior.

  // If a collection is selected, add the collections URI part
  if (!!coll) uriParts.push(`collections/${coll.key}`);
}

if (!collection) {
  // Add the item URI part
  uriParts.push(`items/${targetItem.key}`);
}

// Join the parts together
let uri = uriParts.join("/");

// Add the URI parameters
if (uriParams) {
  uri += uriParams;
}

if (useNoteLink && item?.isNote() && Zotero.BetterNotes) {
  uri = Zotero.BetterNotes.api.convert.note2link(item);
}

// Format the link and copy it to the clipboard
const clipboard = new Zotero.ActionsTags.api.utils.ClipboardHelper();
if (linkType == "html") {
  clipboard.addText(`<a href="${uri}">${linkText}</a>`, "text/unicode");
} else if (linkType == "md") {
  clipboard.addText(`[${linkText}](${uri})`, "text/unicode");
} else {
  clipboard.addText(uri, "text/unicode");
}

clipboard.addText(`<a href="${uri}">${linkText}</a>`, "text/html");

clipboard.copy();

return `[Copy Zotero Link] link ${uri} copied.`;
```
