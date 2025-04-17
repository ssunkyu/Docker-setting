# Docker Setup Guide

## 1. Install Docker

Update package index and install required packages:

```bash
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
```

Add Docker's official GPG key and repository:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

Install Docker and verify:

```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo systemctl status docker
```

Test installation:

```bash
sudo docker run hello-world
```

### Run Docker Without Root

Add user to Docker group:

```bash
sudo usermod -aG docker $USER
newgrp docker
```

Verify group membership:

```bash
groups
```

## 2. Download Ubuntu with CUDA

Find images at: [NVIDIA CUDA Tags](https://hub.docker.com/r/nvidia/cuda/tags)

Run a container with GPU support:

```bash
docker run --name [container_name] -itd --gpus '"device=[gpu_device_numbers]"' -e NVIDIA_VISIBLE_DEVICES=[gpu_device_numbers] --shm-size=[RAM_size] -v [/your/directory]:/workspace [image] /bin/bash
```

Example:

```bash
docker run --name song -itd --gpus '"device=2,3"' -e NVIDIA_VISIBLE_DEVICES=2,3 --shm-size=32G -v /media/seonkyu/WORKSPACE:/workspace nvidia/cuda:11.2.2-devel-ubuntu20.04 /bin/bash
```

### Docker Run Options

- `--name <container_name>`: Specify container name
- `-p <host_port>:<container_port>`: Map ports
- `-v <host_path>:<container_path>`: Mount volume
- `--net=<network_name>`: Connect to network
- `-e <env_var>=<value>`: Set environment variable
- `-d`: Run in background
- `-i`: Attach terminal
- `-t`: Enable special keys

## 3. Reference

- [Docker Installation Guide](https://haesoo9410.tistory.com/380)
