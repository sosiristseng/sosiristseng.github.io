---
title: Git submodule

tags:
  - git
  - devops
---

Frequently used commands for Git submodules.

- [gitaarik's Gist](https://gist.github.com/gitaarik/8735255)
- [Git docs](https://git-scm.com/docs/gitsubmodules)

## Add a submodule

TO add the reference to another git project as a submoule:

```sh
git submodule add <url> <path>
git submodule update --init --recursive
```

Alternatively, you can use GUI tools like or GitHub desktop. They download and initiate submodules automatically.

Add you will see the file `.gitmodules` with information about the submodule(s). For instance,

``` title=".gitmodules"
[submodule "themes/DoIt"]
	path = themes/DoIt
	url = https://github.com/HEIGE-PCloud/DoIt.git
```

## Track a specific branch in the submodule

With `-b <branchname>` option

```sh
git submodule add -b <branchname> <url> <path>
```

Or `set-branch -b <branchname>` if you already have added a submodule

```sh
git submodule set-branch -b <branchname> <path>
```

## Update all Git submodules to the latest commit

From a [stackOverflow post](https://stackoverflow.com/questions/5828324/update-git-submodule-to-latest-commit-on-origin/5828396#5828396) and [Git docs](https://git-scm.com/docs/git-submodule#Documentation/git-submodule.txt-update--init--remote-N--no-fetch--no-recommend-shallow-f--force--checkout--rebase--merge--referenceltrepositorygt--depthltdepthgt--recursive--jobsltngt--no-single-branch--filterltfilterspecgt--ltpathgt82308203)

```sh
git submodule update --remote --merge
```

For automated updates by bots, see [automatic dependency update](../auto-deps-update.md).

## Remove a submodule

From [Git docs](https://git-scm.com/docs/gitsubmodules)

```sh
# Remove submodule from config
git submodule deinit <path>
# Delete submodule tracking data
git rm <submodule path> && git commit
# Complete removal
rm -rf $GIT_DIR/modules/<name>/
```
