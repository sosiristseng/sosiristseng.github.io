---
title: Setup NodeJS in GitHub actions
tags:
  - github
  - nodejs
  - devops
---

The https://github.com/actions/setup-node action installs Node.js and can cache package dependencies. Therefore, the `cache` action is not required.

```yaml
steps:
- uses: actions/checkout@v3
- uses: actions/setup-node@v4
  with:
    node-version: 'lts/*'
    cache: 'npm'
- run: npm ci
- run: npm test
```

The https://github.com/bahmutov/npm-install action does package caching and runs `npm ci` without additional settings.

```yaml
steps:
- uses: bahmutov/npm-install@v1
```
