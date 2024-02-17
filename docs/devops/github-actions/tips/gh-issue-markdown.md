---
title: Convert GitHub issues to a markdown file

tags:
  - markdown
  - github
---

The Python package https://github.com/mattduck/gh2md exports Github repository issues and pull requests to a single, readable markdown file.

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
        token: ${{ secrets.PERSONAL_ACCESS_TOKEN }}
        fetch-depth: 0             # otherwise, you will failed to push refs to dest repo.
    - uses: actions/setup-python@v2
      with:
        python-version: '3.x'
    - name: Install GitHub Issue to Markdown
      run:  pip install gh2md
    - name: Backup github issues into separate markdown files
      env:
        GITHUB_ACCESS_TOKEN: ${{ secrets.PERSONAL_ACCESS_TOKEN }}
      run: |
        rm -rf issues/ || true
        gh2md --multiple-files -I --no-prs --no-closed-prs $GITHUB_REPOSITORY issues/
    - name: Install mmv
      run: sudo apt update && sudo apt install -y mmv
    - name: Modify markdown file names
      working-directory: issues
      run: mmv '*.*.issue.*.md' '#2.md'
    - name: Commit files
      uses: stefanzweifel/git-auto-commit-action@v5
      with:
        commit_message: Backup Issues
```
