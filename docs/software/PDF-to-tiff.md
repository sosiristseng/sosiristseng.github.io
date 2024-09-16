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

**Ubuntu**

```sh
sudo apt install poppler-utils
```

**conda**

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

## ImageMagick

### Install

**Ubuntu**

```sh
sudo apt install imagemagick
```

**Windows**

```powershell
choco install -y imagemagick
```

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
