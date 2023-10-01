---
title: Git Operations in GitLab CICD
draft: false
tags:
  - gitlab
  - git
  - devops
---
How to git commit, add, push, and create merge requests (MRs) in GitLab CI/CD.

- [GitLab forum post about SSH access](https://forum.gitlab.com/t/is-it-possible-to-commit-artifacts-into-the-git/22218/7)
- [thacoon's blog about PAT access](https://thacoon.com/posts/gitlab-ci-auto-dependency-update/)
## Using SSH keys

> [!warning]
> Currently the private key cannot be masked out of the box and one has to use base64 encoding/decoding.

You can use a pair of SSH keys to access a git repository
- The private key would be a [CI/CD project variable](https://docs.gitlab.com/ee/ci/variables/#add-a-cicd-variable-to-a-project)
- The public key would be a [deploy key](https://docs.gitlab.com/ee/user/project/deploy_keys/)

You also need additional steps to setup a SSH client in the pipeline.

```yaml
before_script:
   # apt-get applies to Debain-based images. Change the package manager if needed.
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

## Using a personal access token (PAT)

Compared to SSH, using a [personal access token (PAT)](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html) with `write repo` right might be simpler. In the following example, the PAT is stored as a masked CI/CD variable `GIT_PUSH_TOKEN`.

```yaml
script:
  - bash update.sh
  - |
    if [ -n $(git status --porcelain) ]; then
        echo "Commiting updates"
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
        echo "Commiting updates"
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

## Synchronize GitLab repo to GitHub

How to mirror GitLab repositories to GitHub with deploy SSH keys. Assuming you have two identical repositories on GitLab and GitHub each (you can do this by importing one's repo to the other)

### On the GitLab side

1. In the GitLab repo, go to `Settings`/`Repository`/`Mirroring repositories` and set `Git repository URL` as `ssh://git@github.com/<namespace>/<repo>.git`. e.g. `ssh://git@github.com/sosiristseng/docker-python-julia.git`
![](https://user-images.githubusercontent.com/40054455/153238097-4266f124-b5ef-4fda-82ea-060d79f1ba09.png)

> [!warning]
> The GitHub button gives `git@github.com:<namespace>/<repo>.git` as the repo URL, one should change it to `ssh://git@github.com/<namespace>/<repo>.git` for GitLab to access the repository.

2. Set `Mirror direction` to push.
![](https://user-images.githubusercontent.com/40054455/153238559-7d3beccd-c951-4244-aaa4-cd6375ae370c.png)

3. Set `Authentication method` to SSH public key. Optionally you can click `Detect host keys`.
![](https://user-images.githubusercontent.com/40054455/153239073-bd49113f-838f-4e07-a6d7-dc668bdf76ba.png)

4. (Optionally) check "Keep divergent refs" to prevent force pushes and/or "Mirror only protected branches" for a cleaner GitHub mirror.
5. Click `Mirror repository`.
6. Copy the SSH public key (the middle button) and go to the GitHub mirror repo.
![](https://user-images.githubusercontent.com/40054455/153239908-97df111e-c342-4185-86f9-c71b62ab30b8.png)

### On the GitHub side

In the Github mirror repository, go to `Settings`/`Deploy keys` and add deploy key.

![](https://user-images.githubusercontent.com/40054455/153240371-f937970d-84c4-4c9e-a44c-d7af5b1d3f91.png)

Paste the SSH public key copied from the GitLab source. Give it a title, allow write access, click `add key` to finish this step, and viola.

![](https://user-images.githubusercontent.com/40054455/153240939-2ac0e15b-52e7-48ed-9b11-90e4f4fa18c5.png)
