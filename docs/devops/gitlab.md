---
title: GitLab
date: 2024-04-25
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

This will create 4 jobs with a combination of a custom message and a specific Python image.

**See also** [the blog post by Michael Friedrich](https://dnsmichi.at/2021/09/23/efficient-pipelines-gitlab-ci-cd-parallel-matrix-builds-reference/) for more parallel matrix build with GitLab CI/CD.

## Replace old `only/except` with new `rules` to include or exclude jobs in pipelines

[GitLab CI/CD `rules` reference](https://docs.gitlab.com/ee/ci/yaml/#rules)

> [!NOTE]
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
    - myWS
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

## Git Operations in GitLab CI/CD

### Using SSH keys

> [!WARNING]
> Currently the private key cannot be masked and base64 encoding/decoding is needed.

You can use a pair of SSH keys to access a git repository
- The private key would be a [CI/CD project variable](https://docs.gitlab.com/ee/ci/variables/#add-a-cicd-variable-to-a-project)
- The public key would be a [deploy key](https://docs.gitlab.com/ee/user/project/deploy_keys/)

You also need additional steps to setup a SSH client in the pipeline.

```yaml
before_script:
   # apt-get applies to Debian-based images. Change the package manager if needed.
  - 'which ssh-agent || ( apt-get update -qy && apt-get install openssh-client -qqy )'
  - 'which git || ( apt-get update -qy && apt-get install git -qqy )'
  - eval `ssh-agent -s`
  - echo "${SSH_PRIVATE_KEY}" | tr -d '\r' | ssh-add - > /dev/null # add ssh key
  - '[[ -f /.dockerenv ]] && echo -e "Host *\n\tStrictHostKeyChecking no\n\n" > ~/.ssh/config'
```

And replace the default HTTP-based git origin with the SSH one.

```yaml
script:
  - git remote rm origin && git remote add origin git@gitlab.com:$CI_PROJECT_PATH.git
```

### Using a personal access token (PAT)

Compared to SSH, using a [personal access token (PAT)](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html) with `write repo` right might be simpler. In the following example, the PAT is stored as a masked CI/CD variable `GIT_PUSH_TOKEN`.

```yaml
script:
  - bash update.sh
  - |
    if [ -n $(git status --porcelain) ]; then
        echo "Committing updates"
        git config --global user.name "${GITLAB_USER_NAME}"
        git config --global user.email "${GITLAB_USER_EMAIL}"
        git add .
        git commit -m "Automated update: $(date '+%Y-%m-%d-%H-%M-%S')"
        git push "https://${GITLAB_USER_NAME}:${GIT_PUSH_TOKEN}@${CI_REPOSITORY_URL#*@}"
        exit;
    else
        echo "no change, nothing to commit"
    fi
```

For a MR pipeline, GitLab provides [git push options](https://docs.gitlab.com/ee/user/project/push_options.html) for merge request settings.

```yaml
script:
  - bash update.sh
  - |
    if [ -n $(git status --porcelain) ]; then
        echo "Committing updates"
        NEW_BR=auto-update-$(date '+%Y-%m-%d-%H-%M-%S')
        git config --global user.name "${GITLAB_USER_NAME}"
        git config --global user.email "${GITLAB_USER_EMAIL}"
        git checkout -b ${NEW_BR}
        git add .
        git commit -m "${NEW_BR}"
        git push "https://${GITLAB_USER_NAME}:${GIT_PUSH_TOKEN}@${CI_REPOSITORY_URL#*@}" \
            -o merge_request.create \
            -o merge_request.target="${CI_DEFAULT_BRANCH}" \
            -o merge_request.merge_when_pipeline_succeeds \
            -o merge_request.remove_source_branch \
            -o merge_request.title="${NEW_BR}" \
            -o merge_request.label="automated update" \
            -o merge_request.assign="${GITLAB_USER_NAME}"
        exit;
    else
        echo "no change, nothing to commit"
    fi
```

### Synchronize GitLab repo to GitHub

Assuming you have two identical repositories on GitLab and GitHub each (you can do this by importing one's repo to the other), the following steps show how to mirror GitLab repositories to GitHub with deploy SSH keys.

#### On the GitLab side

1. In the GitLab repo, go to `Settings`/`Repository`/`Mirroring repositories` and set `Git repository URL` as `ssh://git@github.com/<namespace>/<repo>.git`. e.g. `ssh://git@github.com/sosiristseng/docker-python-julia.git`
![](https://user-images.githubusercontent.com/40054455/153238097-4266f124-b5ef-4fda-82ea-060d79f1ba09.png)

> [!WARNING]
> The GitHub button gives `git@github.com:<namespace>/<repo>.git` as the repo URL, one should change it to `ssh://git@github.com/<namespace>/<repo>.git` for GitLab to access the repository.

2. Set `Mirror direction` to push.
![](https://user-images.githubusercontent.com/40054455/153238559-7d3beccd-c951-4244-aaa4-cd6375ae370c.png)

3. Set `Authentication method` to SSH public key. Optionally you can click `Detect host keys`.
![](https://user-images.githubusercontent.com/40054455/153239073-bd49113f-838f-4e07-a6d7-dc668bdf76ba.png)

4. (Optionally) check "Keep divergent refs" to prevent force pushes and/or "Mirror only protected branches" for a cleaner GitHub mirror.
5. Click `Mirror repository`.
6. Copy the SSH public key (the middle button) and go to the GitHub mirror repo.
![](https://user-images.githubusercontent.com/40054455/153239908-97df111e-c342-4185-86f9-c71b62ab30b8.png)

#### On the GitHub side

In the Github mirror repository, go to `Settings`/`Deploy keys` and add deploy key.

![](https://user-images.githubusercontent.com/40054455/153240371-f937970d-84c4-4c9e-a44c-d7af5b1d3f91.png)

Paste the SSH public key copied from the GitLab source. Give it a title, allow write access, click `add key` to finish this step, and viola.

![](https://user-images.githubusercontent.com/40054455/153240939-2ac0e15b-52e7-48ed-9b11-90e4f4fa18c5.png)
