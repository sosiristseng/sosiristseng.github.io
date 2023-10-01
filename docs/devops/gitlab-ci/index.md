---
title: Gitlab CICD tips
draft: 
tags:
  - gitlab
  - devops
  - python
  - git
  - conda
---
[GitLab CI/CD](https://docs.gitlab.com/ee/ci/) is a tool built into GitLab for software development for Continuous Integration (CI) and Continuous Delivery/Deployment (CD).

- [GitLab CI/CD documentation](https://docs.gitlab.com/ee/ci/)
- [How to: Include pipeline files](https://docs.gitlab.com/ee/ci/yaml/index.html#include)

## Parallel Matrix build

Test and build in parallel with matrix build in Gitlab CI/CD.

For example,

```yaml title=".gitlab-ci.yml"
test:
  image: $IMAGE
  script:
    - echo $MSG
    - python -V
  parallel:
    matrix:
      # First cartesian set of parameters
      - IMAGE: ['python:3.6-alpine', 'python:3.7-alpine']
        MSG: ['Test1', 'Test2']
      # Second cartesian set of parameters
```

This will creat 4 jobs with a combination of a custom message and a specific Python image.

**See also** [the blog post by Michael Friedrich](https://dnsmichi.at/2021/09/23/efficient-pipelines-gitlab-ci-cd-parallel-matrix-builds-reference/) for more parallel matrix build with GitLab CI/CD.

## Replace old `only/except` with new `rules` to include or exclude jobs in pipelines

[GitLab CI/CD `rules` reference](https://docs.gitlab.com/ee/ci/yaml/#rules)

> [!note]
> Rules cannot be used together with only/except. Otherwise, GitLab will return a `key may not be used with rules` error.

### only run if this is a scheduled pipeline

```yaml title=".gitlab-ci.yml"
scheduled-update:
  # only run if this is a scheduled pipeline
  rules:
    - if: $CI_PIPELINE_SOURCE == "schedule"
```

### Run upon push

```yaml title=".gitlab-ci.yml"
push-job:
  rules:
    - if: $CI_PIPELINE_SOURCE == "push"
```

### Run upon merge request

```yaml title=".gitlab-ci.yml"
merge-request:
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
```

### Run only for the commits in the default branch

```yaml title=".gitlab-ci.yml"
# GitLab pages job
pages:
  rules:
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
```

### Run only for tags

```yaml title=".gitlab-ci.yml"
pages:
  rules:
    - if: $CI_COMMIT_TAG
```

## Choose a specific runner

Use `tags` to tun jobs in a specific runner e.g., your self-hosted GitLab runner in the workstation.

```yaml title=".gitlab-ci.yml"
run-custom:
  tags:
    - myworkstation
  script:
    - echo "Running in my workstation."
```

## Create a release

[Create a release with GitLab CI/CD pipelines](https://docs.gitlab.com/ee/user/project/releases/#create-a-release) with the `release-cli` docker image:

```yaml title=".gitlab-ci.yml"
release_job:
  stage: release
  image: registry.gitlab.com/gitlab-org/release-cli:latest
  rules:
    - if: $CI_COMMIT_TAG                  # Run this job when a tag is created manually
  script:
    - echo "Running the release job."
  release:
    name: "Release $CI_COMMIT_TAG"
    description: "Release created using the release-cli."
```

## Cache Conda Packages

We can cache conda packages by setting `CONDA_PKGS_DIRS` environment variable inside the project folder (`CI_PROJECT_DIR`) so that the GitLab runner can cache these dependencies.

- [GitLab CICD: caching](https://docs.gitlab.com/ee/ci/caching/)
- [conda: managing environments](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)

```yaml title=".gitlab-ci.yml"
image: condaforge/miniforge3:latest

variables:
  CONDA_PKGS_DIRS: "${CI_PROJECT_DIR}/.cache/conda/pkgs"

cache:
  - key:
      files:
        - environment.yml
    paths:
      - .env/
      - .cache/conda/pkgs

before_script:
  - conda env update --prefix ./.env --file environment.yml --prune
  - source activate ./.env
```

Because GitLab only caches files inside the project folder (`CI_PROJECT_DIR`)

- `CONDA_PKGS_DIRS` is set to `${CI_PROJECT_DIR}/.cache/conda/pkgs` to hold the downloaded compressed packages.
- Extracted environment folder is set to `${CI_PROJECT_DIR}/.env` using the `--prefix` option.

Conda will create the runtime environment according to `environment.yml`. The environment folder will be created (if not present) or cached. The option `--prune` means conda will remove unnecessary packages for subsequent caching.
