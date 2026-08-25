---
title: Git
tags:
  - git
  - development
---

[Git](https://git-scm.com/) version control.

## Setup Git

**Windows**

```powershell
choco feature enable -n=useRememberedArgumentsForUpgrades
choco install -y git.install --params "'/NoShellIntegration'"
```

**Ubuntu**

Usually `git` is included in Ubuntu installation. To install the latest version of git:

```sh
sudo add-apt-repository -y ppa:git-core/ppa
sudo apt update && sudo apt install -y git git-lfs
```

After `git` is installed, add user settings.

```sh
# Default is true on Windows machines
git config --global user.name yourname
git config --global user.email yourname@company.com
```

## Settings

See [git config docs](https://git-scm.com/docs/git-config).

### Force Git to use `LF` line endings in Windows

```sh
# Default is true on Windows machines
git config --global core.autocrlf false
git config --global core.eol lf
```

To apply the setting to all files in the repository, run:

```sh
git add --update --renormalize
```

### Rebase settings

```sh
git config --global pull.rebase true
git config --global rebase.autoSquash true
git config --global rebase.autoStash true
```

### Login to GitHub and GitLab via SSH keys

See [this post](../blog/git-ssh-login.md).

## Usage

- [Git reference](https://git-scm.com/docs)
- [Git cheat sheet (pdf)](https://training.github.com/downloads/github-git-cheat-sheet.pdf)
- [When you screw up git](https://ohshitgit.com/)

### What is `HEAD`

`HEAD`: the current state.

### Download (clone) a repository

[Clone](https://git-scm.com/docs/git-clone) a git repo from a remote repository:

```sh
git clone $url
```

Cloning a specific branch:

```sh
git clone $url -b $branchname
```

If there are submodule(s) in the Git repository, use the `--recursive` option to also clone its submodules.

```sh
git clone $url --recursive
```

### Make changes and commit

```sh
git status      # The current state of the repository.
git add <file>  # Add a new or edited file to the staging area. i.e. telling git to track this file
git add -A      # Track all files at once
git commit -m "Commit message"  # Commit staged (added) file
git commit -am "Commit message" # Commit modified files without having to run git add beforehand
git revert <SHA>                # Make a counter commit to undo the changes. The tracked files will go back to the <SHA> commit.
```

### Synchronize with remote

```sh
git fetch # Download objects and refs from another repository without really pull in the changes
git merge # After git fetch, merge the changes done in the remote to the local repo
git push <remote> <branch-name> # Push commits in to remote
git push --set-upstream <remote> <name-of-your-branch>  # Setup remote url before push
git pull <remote>  # Pull changes from the remote
```

### Git Stash

Temporarily storing untracked files.

```sh
git stash -u   # Store current work with untracked files
git stash pop  # Bring stashed work back to the working directory
```

### List Changed Files With Certain Extension(s)

For example, how to find changed PHP files between latest and the commit before it. [source](https://stackoverflow.com/questions/4734300/git-changed-file-names-with-certain-extension)

```bash
git diff --name-only HEAD~1 HEAD '**/*.php'
```

If the shell does not support the glob pattern, use `grep`

```bash
git diff --name-only HEAD~1 HEAD | grep .php
```

### Work with branches

```sh
git branch <branch_name>    # Create a new branch
git branch -a               # List all branches
git branch -d <branch_name> # Delete a branch

git checkout <branch_name>    # checkout an existing branch
git checkout -b <branch_name> # Create a new branch and checkout it

git switch <branch_name>    # Switch to a specified branch. If the branch name does not exist, create one.
git merge  <branch_name>    # Merge the branch into the current branch
```

### Reset

- Mixed reset (default): discard untracked files, but the changed files are preserved but not marked for commit.
- Hard reset: Resets the index and working tree. Any changes to tracked files in the working tree since `commit` are discarded.
- Soft reset: Does not touch the index file or the working tree at all (but resets the head to `commit`)

```sh
git reset --hard $SHA   # Reset git history to a specific commit
git reset HEAD~         # Reset state to the previous commit (~)
```

### Submodules

Frequently used commands for Git submodules.

- [gitaarik's Gist](https://gist.github.com/gitaarik/8735255)
- [Git docs](https://git-scm.com/docs/gitsubmodules)

#### Add a submodule

TO add the reference to another git project as a submodule:

```sh
git submodule add $url $path
git submodule update --init --recursive
```

Alternatively, you can use GUI tools like or GitHub desktop. They download and initiate submodules automatically.

Add you will see the file `.gitmodules` with information about the submodule(s). For instance,

```txt {filename=".gitmodules"}
[submodule "themes/DoIt"]
	path = themes/DoIt
	url = https://github.com/HEIGE-PCloud/DoIt.git
```

#### Track a specific branch in the submodule

With `-b $branch` option

```sh
git submodule add -b $branch $url $path
```

Or `set-branch -b  $branch` if you already have added a submodule

```sh
git submodule set-branch -b  $branch $path
```

#### Update all Git submodules to the latest commit

From a [stackOverflow post](https://stackoverflow.com/questions/5828324/update-git-submodule-to-latest-commit-on-origin/5828396#5828396) and [Git docs](https://git-scm.com/docs/git-submodule#Documentation/git-submodule.txt-update--init--remote-N--no-fetch--no-recommend-shallow-f--force--checkout--rebase--merge--referenceltrepositorygt--depthltdepthgt--recursive--jobsltngt--no-single-branch--filterltfilterspecgt--ltpathgt82308203)

```sh
git submodule update --remote --merge
```

For automated updates by bots, see [automatic dependency update](../../../blog/github/gha-auto-deps-update.md).

#### Remove a submodule

From [Git docs](https://git-scm.com/docs/gitsubmodules)

```sh
# Remove submodule from config
git submodule deinit $path
# Delete submodule tracking data
git rm <submodule path> && git commit
# Complete removal
rm -rf $GIT_DIR/modules/$name/
```

### Orphan branches

Orphan branches are unrelated to other branches in repo history. The most common example is the `gh-pages` branch holding built webpages for GitHub pages.

```sh
git branch --orphan <branch_name>  # Create a orphan branch
```

### Remove files completely

In case you have committed big binary file(s) or sensitive data into your git repo and want to remove them completely.

[filter-repo](https://github.com/newren/git-filter-repo) for git is a `filter-branch` replacement for rewriting history written in a single-file python script.

To remove files that are larger than 100 MB.

```sh
git filter-repo --strip-blobs-bigger-than 100M
```

To remove a big binary module

```sh
git filter-repo --path src/ --to-subdirectory-filter my-module --tag-rename '':'my-module-'
```

To remove sensitive content

```sh
git filter-repo --use-base-name --path $SENSITIVE_FILE --invert-paths
```

### Erase all history

Erase all commits and history in the Git repo to start over with all the current files. This also clears big file records in the Git database.

```sh
git checkout --orphan newBranch  # Create an orphan branch to hold the files
git add -A  && git commit        # Add all files and commit them
git branch -D main               # Deletes the main branch
git branch -m main               # Rename the current orphan branch to main
git push -f origin main          # Force push main branch to remote (e.g. github)
git gc --aggressive --prune=all  # Remove the old files in the database
```
