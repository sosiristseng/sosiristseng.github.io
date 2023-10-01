---
title: Git Commands
draft: false
tags:
  - git
  - devops
---
Sources:

- [Git reference](https://git-scm.com/docs)
- [Git cheatsheet (pdf)](https://training.github.com/downloads/github-git-cheat-sheet.pdf)
- [When you screw up git](https://ohshitgit.com/)

## Ordinary workflows

`HEAD`: the current state of the repo.

### Download a repository

[Clone](https://git-scm.com/docs/git-clone) a git repo from a remote repository:

```sh
git clone <url>
```

Checking out a perticular branch:

```sh
git clone <url> -b <branchname>
```

If there are submodule(s) in the Git repository, you might want to clone them as well using the `--recursive` option.

```sh
git clone <url> --recursive
```

You might wan to use [[ssh-login-git]].
### Make changes and commit

```sh
git status      # The current state of the repository.

git add <file>  # Add a new or edited file to the staging area. i.e. telling git to track this file

git add -A      # Track all files at once

git commit -m "Commit message"  # Commit staged (added) file

git commit -am "Commit message" # Commit modified files without having to run git add beforehand

git revert <SHA>                # Make a counter commit to undo the changes. The tracked files will go back to the <SHA> commit.
```

### Synchronize with remote: Push and pull

```sh
git fetch # Download objects and refs from another repository without really pull in the changes

git merge # After git fetch, merge the changeds done in the remote to the local repo

git push <remote> <branch-name> # Push commits in to remote

git push --set-upstream <remote> <name-of-your-branch>  # Setup remote url before push

git pull <remote>  # Pull changes from the remote
```

### Stash

To temporarily store untracked files.

```sh
git stash -u   # Store current work with untracked files

git stash pop  # Bring stashed work back to the working directory
```

## Work with branches

```sh
git branch <branch_name>    # Create a new branch

git branch -a               # List all branches

git branch -d <branch_name> # Delete a branch

git checkout <branch_name>    # checkout an existing branch

git checkout -b <branch_name> # Create a new branch and checkout it

git switch <branch_name>    # Switch to a specified branch. If the branch name does not exist, create one.

git merge  <branch_name>    # Merge the branch into the current branch
```

### Orphan branches

Orphan branches are unrelated to others in history. For example, `gh-pages` branch dedicated to GitHub pages.

```sh
git branch --orphan <branchname>  # Create a orphan branch
```
