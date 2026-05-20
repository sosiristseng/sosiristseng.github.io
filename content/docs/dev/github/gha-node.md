---
title: NodeJS in GitHub actions
date: 2024-04-25
tags:
  - github
  - nodejs
---

The https://github.com/actions/setup-node action installs Node.js and caches package dependencies.

<!--more-->

```yaml
steps:
- uses: actions/checkout@v4
- uses: actions/setup-node@v4
  with:
    node-version: 'lts/*'
    cache: 'npm'
- run: npm ci
- run: npm test
```
