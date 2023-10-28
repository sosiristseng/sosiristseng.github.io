---
title: pipeview
tags:
  - tiff
  - document
  - linux
  - windows
---

Convert `pdf` files to `tiff` images with `pdftoppm` or `ghostscript`.

## pdftoppm

[^2]: https://www.linuxuprising.com/2019/03/how-to-convert-pdf-to-image-png-jpeg.html
[^3]: https://jdhao.github.io/2019/11/14/convert_pdf_to_images_pdftoppm/
[^4]: https://officeguide.cc/linux-pdftoppm-convert-pdf-to-jpg-png-tiff-image-tutorial-examples/

To install `pdftoppm` (included in `poppler-utils`)[^2][^3][^4]

=== "Ubuntu"

    ```sh
    sudo apt install poppler-utils
    ```

=== "Arch Linux"

    ```sh
    sudo pacman -S poppler-utils
    ```

=== "conda"

    ```sh
    conda install -c conda-forge poppler
    ```

Usage: see [documentation of `pdftoppm`](https://www.mankier.com/1/pdftoppm)

For example, to convert the pdf file to a 300-DPI TIFF image with lzw compression.

```sh
pdftoppm -tiff -tiffcompression lzw -r 300 in.pdf outname
```

## GhostScript and ImageMagick

### Setup

To install GhostScript and ImageMagick

=== "Ubuntu"

    ```sh
    sudo apt install ghostscript imagemagick
    ```

=== "Arch Linux"

    ```sh
    sudo pacman -S ghostscript imagemagick
    ```

=== "Windows"

    ```powershell
    choco install -y ghostscript imagemagick
    ```

!!! note

    For security reasons, PDF read/write operations are disable by default. You enable this function by editing the settings file
   
```xml title="/etc/ImageMagick-7/policy.xml"
<policy domain="coder" rights="read | write" pattern="PDF" />
```

### Command example

How to convert a `pdf` file to a `tiff` one:

```sh
convert -density 300 \
        -compress lzw \
        -background white \
        -alpha remove \
        -trim \
        "image.pdf" "image_%d.tiff"
```
