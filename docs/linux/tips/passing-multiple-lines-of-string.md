---
title: Passing multiple lines of string

tags:
  - linux
  - command-line
---

Use [heredoc](https://en.wikipedia.org/wiki/Here_document) to pass the string as-is between two delimiters (e.g. `EOF`)
```sh
cat << "EOF" >> ~/.xprofile
# ~/.xprofile
export GTK_IM_MODULE=ibus
export QT_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
ibus-daemon -drx
EOF
```

  Will append the following lines in ~/.xprofile:

```sh title=".xprofile"
export GTK_IM_MODULE=ibus
export QT_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
ibus-daemon -drx
```
