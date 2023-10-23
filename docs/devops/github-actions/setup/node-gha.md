---
title: Setup NodeJS in GitHub actions
tags:
  - github
  - nodejs
  - devops

---
The [setup-node](https://github.com/actions/setup-node) action installs Node.js and (optionally) caches package dependencies. Therefore, the `cache` action is not needed.

```yaml
steps:
- uses: actions/checkout@v2
- uses: actions/setup-node@v2
  with:
    node-version: '18'
    cache: 'npm'
- run: npm ci
- run: npm test
```
