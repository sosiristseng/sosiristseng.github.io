---
title: Setup docker in Github actions
date: 2024-04-25
tags:
  - docker
  - github
---

## Building and publishing docker images

- [Docker documentation: Configure GitHub Actions](https://docs.docker.com/ci-cd/github-actions/)
- [How to publish a docker image into the Github package registry](https://docs.github.com/en/actions/publishing-packages/publishing-docker-images)

<!--more-->

```yaml {filename=".github/workflows/docker.yml"}
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

```yaml {filename=".github/workflows/test-container.yml"}
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

### Docker run command

Use the regular [docker run](https://docs.docker.com/engine/reference/commandline/run/) command. Here we use `>` to fold commands in YAML.

```yaml {filename=".github/workflows/test-container.yml"}
name: container
on: push

env:
  IMG: "node:14.15.0-alpine3.12"

jobs:
  node-docker:
    runs-on: ubuntu-latest
    steps:
      - name: Log the node version
        run: >
          docker run -rm -v $(pwd):/tmp -w /tmp
          ${{ env.IMG }}
          bash -c "node -v; cat /etc/os-release"
```
