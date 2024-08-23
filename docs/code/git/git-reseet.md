---
title: Git reset
tags:
  - git
---

- Mixed reset (default): discard untracked files, but the changed files are preserved but not marked for commit.
- Hard reset: Resets the index and working tree. Any changes to tracked files in the working tree since `commit` are discarded.
- Soft reset: Does not touch the index file or the working tree at all (but resets the head to `commit`)

```sh
git reset --hard <SHA>   # Reset git history to a specific commit

git reset HEAD~          # Reset state to the previous commit (~)
```
