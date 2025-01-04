---
title: Purge Git database entirely
tags:
  - git
---

Erase all history in the Git repo to start over with all the current files. This also clears big file records in the Git database.

```sh
git checkout --orphan newBranch  # Create an orphan branch to hold the files
git add -A  && git commit        # Add all files and commit them
git branch -D main               # Deletes the main branch
git branch -m main               # Rename the current orphan branch to main
git push -f origin main          # Force push main branch to remote (e.g. github)
git gc --aggressive --prune=all  # Remove the old files in the database
```
