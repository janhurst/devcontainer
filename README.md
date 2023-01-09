# Jan Hurst's Dev Containers

Public images available at https://hub.docker.com/r/janhurst/devcontainer

The devcontainer definitions here are "base" containers intended to speed up day to day use of VS Code Dev Containers by prebuilding images.

At the moment these are manually built from time to time using the devcontainer cli.

# Getting Started

```
docker pull janhurst/devcontainer:base
```

or use in a Dockerfile or Docker Compose configuration

```
FROM janhurst/devcontainer:base

...
```

# Images

## janhurst/devcontainer:tools

This image is a common set of features that I use regularly in "full stack" workflows. It is intended as a foundation image as (for now) I find building features to be a bit slow.

Installs the following [Dev Container Features](https://containers.dev/features):

- Node
- .NET 6
- Azure CLI
- Docker-in-Docker
- miniforge (conda/mamba)

## janhurst/devcontainer:base

This image builds on top of the `janhurst/devcontainer:tools` image.

Installs or configures the following via Dockerfile:

- sets an optional apt mirror (defaulting to the AU mirror)
- adds the conda path to the sudo "safe" path to allow `sudo conda ...` to work
- installs git, git-lfs, curl, yarn, zsh from apt
- installs a suite of daily driver conda packages into the base conda environment
- installs Azure DevOps credential providers and configures useHttpPath
- configures `ipython` to auto reload modules when running notebook cells
- adds the docker in docker entry points

## janhurst/devcontainer:ml

This image is experimental, it is intended to install Nvidia CUDA and pytorch.
