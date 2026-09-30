---
title: Docker
tags:
  - docker
  - devops
  - linux
  - gpu
---

<!--more-->

- [awesome-docker](https://github.com/veggiemonk/awesome-docker) : A curated list of Docker resources and project.
- [Docker Hub](https://hub.docker.com/) for docker images.

## Install docker engine

Please check [supported versions](https://docs.docker.com/engine/install/ubuntu/) first before adding the repository.

```bash
sudo apt update && sudo apt install -y ca-certificates curl gnupg lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update && sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

## NVIDIA GPU support

1. Setup nvidia driver. See [cuda](cuda.md).
2. Install [the NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html#installation)

```sh
sudo apt install -y --no-install-recommends ca-certificates curl gnupg2
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg
curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
sudo apt update && sudo apt install -y nvidia-container-toolkit
sudo nvidia-ctk runtime configure --runtime=docker
sudo systemctl restart docker
```

## Test docker installation

Test docker

```sh
sudo docker run hello-world
```

Test nvidia GPU support

```sh
sudo docker run --gpus all nvidia/cuda:13.0-base nvidia-smi
```

## (Optional) add a user to the docker group

So you don't have to type `sudo` in docker commands.

```sh
sudo usermod -aG docker $USER
```

Log out and log back in apply the change.

## Default settings for Docker

The `/etc/docker/daemon.json` files holds docker settings.

- `data-root`: You can put the Docker data directory to another partition. (using `/home/docker` in this example)
- `storage-driver`: Set up [BTRFS storage driver](https://docs.docker.com/engine/storage/drivers/btrfs-driver/) if the Docker data directory is in a BTRFS partition.
- `registry-mirrors`: Set up [Google's pull-through cache](https://cloud.google.com/artifact-registry/docs/pull-cached-dockerhub-images) to work around the DockerHub's [pull rate limit](https://www.docker.com/blog/scaling-docker-to-serve-millions-more-developers-network-egress/).

Edit `/etc/docker/daemon.json` for the following options

```json {filename="/etc/docker/daemon.json"}
{
  "data-root": "/home/docker",
  "registry-mirrors": ["https://mirror.gcr.io"],
  "storage-driver": "btrfs"
}
```

Then run the following command to apply new docker daemon settings.

```bash
sudo service docker restart
```

You can see the new settings using this command

```sh
sudo docker info
```

## Maintenance

[Pruning unused docker objects](https://docs.docker.com/engine/manage-resources/pruning/)

For example, removing all unused docker things.
```sh
docker system prune
```

## Documentations and Tutorials for Docker

- Dockerfile [best practice](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices)
- [Production-ready Docker packaging for Python developers](https://pythonspeed.com/docker/).

## Docker and GitHub actions

- [Docker documentation: Configure GitHub Actions](https://docs.docker.com/ci-cd/github-actions/)
- [How to publish a docker image into the Github package registry](https://docs.github.com/en/actions/publishing-packages/publishing-docker-images)
- [Running jobs in a container](https://docs.github.com/en/actions/using-jobs/running-jobs-in-a-container) in GitHub actions.

Or use the regular [docker run](https://docs.docker.com/engine/reference/commandline/run/) command. Here we use `>` to fold commands in YAML.

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
