# Jan Hurst's Dev Containers

Public images available at https://hub.docker.com/r/janhurst/devcontainer

The devcontainer definition here is a "base" container intended to speed up day to day use of VS Code Dev Containers by a prebuilt image.

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

## janhurst/devcontainer:base

This image is a common set of features that I use regularly in "full stack" workflows. It is intended as a foundation image as (for now) I find building features to be a bit slow.

Installs the following [Dev Container Features](https://containers.dev/features):

- Docker-in-Docker
- Node LTS
- .NET 7
- Azure CLI
- miniforge (conda/mamba)
- pipx
- Black, Flake8, Mypy
- Poetry and Hatch
- DVC

and configures the following via the Dockerfile:

- adds the conda path to the sudo "safe" path to allow `sudo conda ...` to work
- configures `ipython` to auto reload modules when running notebook cells
- adds the docker in docker entry points
