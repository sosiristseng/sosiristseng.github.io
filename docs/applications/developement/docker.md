---
title: docker
tags:
  - docker
  - devops
  - linux
  - windows
---

- https://github.com/veggiemonk/awesome-docker : A curated list of Docker resources and project.
- [Docker Hub](https://hub.docker.com/) for docker images.

## Install docker engine

=== "Ubuntu"

    Please check docker's [supported versions](https://docs.docker.com/engine/install/ubuntu/) before adding the docker repo.

    ```bash
    sudo apt-get update &&
    sudo apt-get install -y \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

    sudo apt update && sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
    ```

=== "Arch Linux"

```sh
sudo pacman -S docker
sudo systemctl enable --now docker.service
```

=== "Windows"

    Docker for Windows has [[WSL2]] integration.

    ```powershell
    choco install docker-desktop
    ```

## NVIDIA GPU support

=== "Ubuntu"

    Install [the NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html#installation)

    ```sh
    curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg
    curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
    sudo apt-get update
    sudo apt-get install -y nvidia-container-toolkit
    sudo nvidia-ctk runtime configure --runtime=docker
    sudo systemctl restart docker
    ```

=== "Arch Linux"

    ```sh
    yay -S nvidia-container-toolkit
    sudo systemctl restart docker
    ```

=== "Windows"

    Once a [Windows NVIDIA GPU driver](https://www.nvidia.com/Download/index.aspx?lang=en-us) is installed on the system, CUDA becomes available within WSL 2.

    And install the CUDA toolkit in the WSL (Ubuntu WSL for example)

    ```bash
    # remove the old GPG key
    sudo apt-key del 7fa2af80
    # Insatll Linux CUDA toolkit
    wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-keyring_1.1-1_all.deb
    sudo dpkg -i cuda-keyring_1.1-1_all.deb
    sudo apt-get update
    sudo apt-get -y install cuda
    ```

## Test docker installation

```sh
sudo docker run hello-world

# nvidia GPU support
sudo docker run --gpus all nvidia/cuda:11.0-base nvidia-smi
```

## Tips

### Workaround DockerHub image pull rate limits

DockerHub has [pull rate limits](https://www.docker.com/blog/scaling-docker-to-serve-millions-more-developers-network-egress/) on the unregisterd as weel as the free plan.

To workaround these limits, we can use the [Google cloud cache](https://cloud.google.com/container-registry/docs/pulling-cached-images) for docker images.

Add the following to `/etc/docker/daemon.json`
```json
{
  "registry-mirrors": ["https://mirror.gcr.io"]
}
```
and restart the docker daemon
```sh
sudo service docker restart
```

## Documentations and Tutorials for Docker

- Dockerfile [best practice](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices)
- [Production-ready Docker packaging for Python developers](https://pythonspeed.com/docker/) by Turner-Trauring.

## Docker Utilities

- https://github.com/hadolint/hadolint : Dockerfile linter that helps you build best practice Docker images, validate inline bash, written in Haskell.
- https://github.com/rpardini/docker-registry-proxy : Self-hosted docker registry proxy
