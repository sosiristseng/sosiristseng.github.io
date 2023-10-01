---
title: Convert GitHub issues to a markdown file
draft: false
tags:
  - markdown
  - github
---
The Python package [gh2md](https://github.com/mattduck/gh2md) exports Github repository issues and pull requests to a single, readable markdown file.

```yaml title=".github/workflows/issues2md.yml"
name: Issues2Markdown
on:
  # issues:
  # issue_comment:
  workflow_dispatch: # manually run this workflow
  schedule:
    - cron: "0 0 * * *"  # On 00:00 every day
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
      with:
        fetch-depth: 0             # otherwise, you will failed to push refs to dest repo.
    - uses: actions/setup-python@v2
      with:
        python-version: '3.x'
    - name: Install GitHub Issue to Markdown
      run:  pip install gh2md
    - name: Backup github issues to a markdown file.
      run:  gh2md $GITHUB_REPOSITORY README.md --token ${{ secrets.GITHUB_TOKEN }}
    - name: Add and Commit files
      uses: EndBug/add-and-commit@v7
```
