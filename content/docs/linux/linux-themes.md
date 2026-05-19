---
title: Linux Themes
tags:
  - linux
---

<!--more-->

[Best GTK themes from Its FOSS](https://itsfoss.com/best-gtk-themes/)

## Papirus icon theme and Kvantum SVG engine

- https://github.com/PapirusDevelopmentTeam/papirus-icon-theme
- https://github.com/tsujan/Kvantum : SVG-based theme engine

### Install (Ubuntu)

```sh
sudo add-apt-repository -y ppa:papirus/papirus           # Papirus icon theme
sudo apt update && sudo apt install -y papirus-icon-theme qt5-style-kvantum qt5ct
```

## Materia theme

A clean theme for both KDE and Gnome.

- https://github.com/PapirusDevelopmentTeam/materia-kde
- https://github.com/nana-4/materia-theme

### Install (Ubuntu)

```sh
sudo add-apt-repository -y ppa:papirus/papirus
sudo apt update && sudo apt install materia-gtk-theme materia-kde
```

### Set fonts

Fonts for materia theme:

- To properly display the theme, use a font family that includes Medium weight (e.g. `Roboto` or M+).
- Set the font size to 9.75 (= 13px at 96dpi) or 10.5 (= 14px at 96dpi).

## Qogir theme

https://github.com/vinceliuice/Qogir-theme is a flat Design theme for GTK.

### Install (Ubuntu)

Download and run the install script from https://github.com/vinceliuice/Qogir-theme.
