---
title: Setup NodeJS
tags:
  - github
  - nodejs
  - devops
---

The https://github.com/actions/setup-node action installs Node.js and caches package dependencies.

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
