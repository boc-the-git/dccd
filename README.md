# dccd

[![Shellcheck](https://github.com/loganmarchione/dccd/actions/workflows/main.yml/badge.svg)](https://github.com/loganmarchione/dccd/actions/workflows/main.yml)

Bash tool for Docker Compose that does Continous Deployment (DCCD)

## Overview

I run a small Kubernetes cluster at home where I use [Renovate](https://github.com/renovatebot/renovate) for dependency management and [Flux](https://github.com/fluxcd/flux2) for continuous deployment.

Flux has spoiled me, but I've found nothing like it for my small Docker Compose setup (the stuff that isn't on K8s yet).

DCCD is a bash script that is meant to run via crontab. It checks the specified repo and branch for changes, compares the commits on the remote and local repos, and updates the local repo as needed.

## Requirements

You'll obviously need to have `git` and `docker compose` installed.

Docker Compose files will need to be named `docker-compose.yml` or `docker-compose.yaml`

## Usage

```
    Usage:   ./dccd.sh [OPTIONS]

    Options:
      -b <name>       Specify the remote branch to track (default: main)
      -d <path>       Specify the base directory of the git repository  (required)
      -h              Show this help message
      -l <path>       Specify the path to the log file (default: /tmp/dccd.log)
      -x <path>       Exclude directories matching the specified pattern (relative to the base directory)
      
    Example: ./dccd.sh -b master -d /path/to/git_repo -x ignore_this_directory
```

## Alternatives

* What about [Portainer](https://github.com/portainer/portainer)? Portainer Business Edition does [gitops](https://www.portainer.io/gitops-automation), but I'm trying to remove my dependency on Portainer.
* What about [Watchtower](https://github.com/containrrr/watchtower)? Watchtower only works if the image tag is `latest`, and it checks for updates against a container image repo directly, not against Docker Compose files in a git repo.
* What about [Harbormaster](https://gitlab.com/stavros/harbormaster)? This comes close, but Harbormaster needs a specific configuration and the directory structure of the Docker Compose files has to be setup a specific way.
