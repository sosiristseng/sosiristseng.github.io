---
title: Passing arguments from a text file
tags:
  - linux
  - command-line
---

Using `sed` and `xargs` to pass a list of arguments to a command from a text file.

For example, to install two lists of packages in Ubuntu:

```sh
cat list1.txt list2.txt | sed 's/#.*$//' | xargs sudo apt install
```

- `xargs` takes the output from `sed` as arguments to `apt`
- `sed 's/#.*$//'` filters out text after `#`. So the `list2.txt` can have comments like this

```txt
# Comment
item1
item2  # A comment after an item
    item3  # indent OK
```
