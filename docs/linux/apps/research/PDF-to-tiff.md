---
title: Convert PDF to TIFF
tags:
  - tiff
  - pdf
  - document
  - linux
  - windows
  - research
---

Convert `pdf` files to `tiff` images with `pdftoppm` or `ghostscript`.

## pdftoppm

[^2]: https://www.linuxuprising.com/2019/03/how-to-convert-pdf-to-image-png-jpeg.html
[^3]: https://jdhao.github.io/2019/11/14/convert_pdf_to_images_pdftoppm/
[^4]: https://officeguide.cc/linux-pdftoppm-convert-pdf-to-jpg-png-tiff-image-tutorial-examples/

### Install pdftoppm

To install `pdftoppm` (included in `poppler-utils`)[^2][^3][^4]

=== "Ubuntu"

    ```sh
    sudo apt install poppler-utils
    ```

=== "conda"

    Available in both Windows and Linux.

    ```sh
    conda install -c conda-forge poppler
    ```

### Usage

See [documentation of `pdftoppm`](https://www.mankier.com/1/pdftoppm)

For example, to convert the pdf file to a 300-DPI TIFF image with LZW compression.

```sh
pdftoppm -tiff -tiffcompression lzw -r 300 in.pdf out.tif
```

## GhostScript and ImageMagick

### Install

To install GhostScript and ImageMagick

=== "Ubuntu"

    ```sh
    sudo apt install ghostscript imagemagick
    ```

=== "Windows"

    ```powershell
    choco install -y ghostscript imagemagick
    ```

> [!NOTE]
> For security reasons, PDF read and write operations are disable by default. Enable PDF read and write by editing `/etc/ImageMagick-7/policy.xml`
> ```xml title="/etc/ImageMagick-7/policy.xml"
> <policy domain="coder" rights="read | write" pattern="PDF" />
> ```

### Usage

How to convert a `pdf` file to a `tiff` file:

```sh
magick "image.pdf" -density 300 \
        -compress lzw \
        -background white \
        -alpha remove \
        -trim \
        "image_%d.tiff"
```
