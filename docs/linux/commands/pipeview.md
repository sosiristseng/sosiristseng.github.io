---
title: pipeview
tags:
  - linux
  - command-line
---

pipeview ([`pv`](https://www.geeksforgeeks.org/pv-command-in-linux-with-examples/)) shows transfer speed and/or transfer progress through a Unix pipe.

`pv` works like `cat`. For example,

```sh
# no output
cat file > other_file

# Display progress
pv file > other_file  
```

```sh
# Showing both compression progress and speed
pv file | gzip > file.gz
# Sandwich form, showing speed without progress
cat file | pv | gzip > file.gz
```
