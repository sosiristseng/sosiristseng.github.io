---
title: Heredoc
date: 2024-09-16
tags:
  - linux
  - command-line
---

Use [heredoc](https://en.wikipedia.org/wiki/Here_document) to pass the string as-is between two delimiters (e.g. `EOF`)

<!--more-->

```sh
cat << "EOF" >> ~/.xprofile
# ~/.xprofile
export GTK_IM_MODULE=ibus
export QT_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
ibus-daemon -drx
EOF
```
