---
title: Caching in GitHub actions
tags:
  - github
  - devops
---

## Caching dependencies

The https://github.com/actions/cache action caches dependencies for the execution environment.

```yaml
- name: Cache multiple paths
  uses: actions/cache@v3
  with:
    path: |
      ~/cache
      !~/cache/exclude
    key: ${{ runner.os }}-${{ hashFiles('**/Lockfile') }}
    restore-keys: |
      ${{ runner.os }}-
```

- The `key` is the identifier for writing into the cache. If the `key` stays the same before and after the workflow, the cache will not be updated.
- The `restore-keys` are the identifiers for reading the cache besides the `key`. If there is no matching `key` but a part of it (`restore-keys`) matches, the Github action will still read the cache and update it after the job is done. (since the `key` is different)

### restore and save actions

The `cache` actions could be split into `restore` and `save` steps, leading to a fine-grained behavior.

```yaml
- name: Restore cached Primes
      id: cache-primes-restore
      uses: actions/cache/restore@v3
      with:
        path: |
          path/to/dependencies
          some/other/dependencies
        key: ${{ runner.os }}-primes
#
# //intermediate workflow steps
#
- name: Save Primes
  id: cache-primes-save
  uses: actions/cache/save@v3
  with:
    path: |
      path/to/dependencies
      some/other/dependencies
```

## Cleanup caches

Caches become invalid after 7 days. If you want to clean the cache before that, for example, in closed PR branch, use the `gh` extension.

```yaml
name: Cleanup PR caches
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
