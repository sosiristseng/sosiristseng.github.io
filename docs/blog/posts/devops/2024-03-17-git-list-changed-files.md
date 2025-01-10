---
title: "Git: Changed File Names With Certain Extension"
date: 2024-03-17
tags:
  - git
categories:
  - DevOps
---

For example, how to find changed PHP files between latest and the commit before it: [^SO]

```bash
git diff --name-only HEAD~1 HEAD '**/*.php'
```

If the shell does not support the glob pattern, use `grep`

```bash
git diff --name-only HEAD~1 HEAD | grep .php
```

[^SO]: https://stackoverflow.com/questions/4734300/git-changed-file-names-with-certain-extension
