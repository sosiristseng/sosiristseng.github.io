---
title: docker
tags:
  - docker
  - devops
---

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

Install [the NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html#installation)

```sh
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg
curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
sudo apt update && sudo apt install -y nvidia-container-toolkit
sudo nvidia-ctk runtime configure --runtime=docker
sudo systemctl restart docker
```

## Test docker installation

```sh
sudo docker run hello-world

# nvidia GPU support
sudo docker run --gpus all nvidia/cuda:12.0-base nvidia-smi
```

## (Optional) add to docker group

So you don't have to use `sudo` on docker commands.

```sh
sudo usermod -aG docker $USER
```

And then log out and log back in.

## (Optional) settings for Docker

- `data-root`: Put the Docker data directory to another partition. (`/home/docker` in this example)
- `registry-mirrors`: Set up [Google's pull-through cache](https://cloud.google.com/artifact-registry/docs/pull-cached-dockerhub-images) to work around the DockerHub's [pull rate limit](https://www.docker.com/blog/scaling-docker-to-serve-millions-more-developers-network-egress/).
- `storage-driver`: Set up [BTRFS storage driver](https://docs.docker.com/engine/storage/drivers/btrfs-driver/) if the Docker data directory is in a BTRFS partition.

Edit `/etc/docker/daemon.json`, add the following entries

```json title="/etc/docker/daemon.json"
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

You can see the new settings:

```sh
sudo docker info
```

## Documentations and Tutorials for Docker

- Dockerfile [best practice](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices)
- [Production-ready Docker packaging for Python developers](https://pythonspeed.com/docker/).

## Docker Utilities

- https://github.com/hadolint/hadolint : Dockerfile linter that helps you build best practice Docker images, validate inline bash, written in Haskell.
- https://github.com/rpardini/docker-registry-proxy : Self-hosted docker registry proxy
