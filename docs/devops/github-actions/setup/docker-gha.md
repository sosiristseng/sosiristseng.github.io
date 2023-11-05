---
title: Setup docker in GitHub actions
tags:
  - docker
  - github
  - devops
---

## Building and publishing docker images

- [Docker documentation: Configure GitHub Actions](https://docs.docker.com/ci-cd/github-actions/)
- [How to publish a docker image into the Github package registry](https://docs.github.com/en/actions/publishing-packages/publishing-docker-images)


```yaml title=".github/workflows/docker.yml"
name: Create and publish a Docker image

on:
  push:
    branches: ['main']

env:
  REGISTRY: ghcr.io
  IMAGE_NAME: ${{ github.repository }}

jobs:
  build-and-push-image:
    runs-on: ubuntu-latest

    # GITHUB_TOKEN permissions
    permissions:
      contents: read
      packages: write

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2
      - name: Setup Buildx
        uses: docker/setup-buildx-action@v2
      - name: Log in to the Container registry
        uses: docker/login-action@v1
        with:
          registry: ${{ env.REGISTRY }}
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - name: Extract metadata (tags, labels) for Docker
        id: meta
        uses: docker/metadata-action@v3
        with:
          images: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}

      - name: Build and push Docker image
        uses: docker/build-push-action@v2
        with:
          context: .
          push: true
          tags: ${{ steps.meta.outputs.tags }}
          labels: ${{ steps.meta.outputs.labels }}
```

## Run docker containers in Github actions

### Use container keyword

[Running jobs in a container](https://docs.github.com/en/actions/using-jobs/running-jobs-in-a-container) in GitHub actions.

```yaml title=".github/workflows/test-container.yml"
name: container
on: push

jobs:
  node-docker:
    runs-on: ubuntu-latest
    container:
      image: node:14.15.0-alpine3.12
    steps:
      - name: Log the node version
        run: |
          node -v
          cat /etc/os-release
```

### Docker run action

The https://github.com/addnab/docker-run-action runs a specific step in a docker container.

```yaml title=".github/workflows/run-container.yml"
- uses: docker/build-push-action@v2
  with:
    tags: test-image:latest
    push: false
- uses: addnab/docker-run-action@v3
  with:
    image: test-image:latest
    options: -w /tmp -v ${{ github.workspace }}:/tmp -e ABC=123
    run: |
      echo "Running Script"
      ./run-script
```

You need to setup proper mount point(s) to receive execution result in later steps.
