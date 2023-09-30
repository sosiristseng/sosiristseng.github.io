---
title: Caching in GitHub actions
draft:
tags:
  - github
  - devops
---
## Caching dependencies

The <https://github.com/actions/cache> action caches dependencies for the execution environment.

```yaml
- name: Cache multiple paths
  uses: actions/cache@v3
  with:
    path: |
      ~/cache
      !~/cache/exclude
    key: ${{ runner.os }}-${{ hashFiles('**/lockfiles') }}
    restore-keys: |
      ${{ runner.os }}-
```

- `key` is the identifier for writing into the cache. If `key` stays the same before and after the workflow, the cache will not be updated.
- `restore-keys` are the identifiers for reading the cache besides `key`. If there is no matching `key` but a part of it (`restore-keys`) matches, the Github action will still read the cache and upadte it after the job is done. (since the `key` is different)

### Caching in programming languages

Some github actions setting up runtime enviroments already have caching actions built-in; thus explicit cache actions is not required.

- Python: the <https://github.com/actions/setup-python> action caches pip, poetry, and pipenv packages.
- Julia: the <https://github.com/julia-actions/cache> action caches Julia artifacts, packages, and registries.
- NodeJS: the <https://github.com/actions/setup-node> action caches NodeJS package dependancies.

## Cleanup caches

Use the `gh` extension to manually clean up caches.

```yml
name: Cleanup caches
on:
  pull_request:
    types:
      - closed
  workflow_dispatch:

jobs:
  cleanup:
    permissions:
      actions: write
    runs-on: ubuntu-latest
    steps:
      - name: Check out code
        uses: actions/checkout@v3
      - name: Cleanup
        run: |
          gh extension install actions/gh-actions-cache
          REPO=${{ github.repository }}
          BRANCH=${{ github.ref }}

          echo "Fetching list of cache key"
          cacheKeysForPR=$(gh actions-cache list -R $REPO -B $BRANCH | cut -f 1 )

          ## Setting this to not fail the workflow while deleting cache keys.
          set +e
          echo "Deleting caches..."
          for cacheKey in $cacheKeysForPR
          do
              gh actions-cache delete $cacheKey -R $REPO -B $BRANCH --confirm
          done
          echo "Done"
        env:
          GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
