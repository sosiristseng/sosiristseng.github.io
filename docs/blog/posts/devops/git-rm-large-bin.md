---
title: Removing large binary blobs in the git tree
date: 2024-03-20
tags:
  - git
---

[Git filter-repo](https://github.com/newren/git-filter-repo) is a `filter-branch` replacement for rewriting history written in a single-file python script.

To wipe large binary files entirely:

```sh
git filter-repo --strip-blobs-bigger-than 100M
```

<!-- more -->

Bonus: Remove sensitive content

```sh
git filter-repo --use-base-name --path id_dsa --path id_rsa --invert-paths
```

```sh
git filter-repo --replace-text passwords.txt
```
