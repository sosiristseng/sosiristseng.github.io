---
title: Change git histories
tags:
  - git
---

## Git reset

- Mixed reset (default): discard untracked files, but the changed files are preserved but not marked for commit.
- Hard reset: Resets the index and working tree. Any changes to tracked files in the working tree since `commit` are discarded.
- Soft reset: Does not touch the index file or the working tree at all (but resets the head to `commit`)

```sh
git reset --hard <SHA>   # Reset git history to a specific commit

git reset HEAD~          # Reset state to the previous commit (~)
```

## Removing large binary blobs

[Git filter-repo](https://github.com/newren/git-filter-repo) is a `filter-branch` replacement for rewriting history written in a single-file python script.

To wipe large binary files entirely:

```sh
git filter-repo --strip-blobs-bigger-than 100M
```

Bonus: Remove sensitive content

```sh
git filter-repo --use-base-name --path id_dsa --path id_rsa --invert-paths
```

```sh
git filter-repo --replace-text passwords.txt
```

## Purge Git database entirely

Erase all history in the Git repo to start over with all the current files. This also clears big file records in the Git database.

```sh
git checkout --orphan newBranch  # Create an orphan branch to hold the files
git add -A  && git commit        # Add all files and commit them
git branch -D main               # Deletes the main branch
git branch -m main               # Rename the current orphan branch to main
git push -f origin main          # Force push main branch to remote (e.g. github)
git gc --aggressive --prune=all  # Remove the old files in the database
```
