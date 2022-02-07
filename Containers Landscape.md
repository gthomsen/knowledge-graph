Tags: #software-engineering 

Junk drawer for information on containers and non-Docker run-times.

[Hacker News article about using containers on Mac without Docker Desktop](https://news.ycombinator.com/item?id=30116433).  Motivated by Docker's licensing change coming in March 2022.

Additional [blog post](https://matt-rickard.com/docker-desktop-alternatives/) covering alternatives:
- Minikube
- Podman
- Colima
- K3s
- microk8s
- Kind

# Runtimes
## Podman
Does not require privileges to run, either building or installation.

## Singularity
Does not require privileges to run and maps a non-trivial amount of the host's environment (uid/gid, directories, and environment variables) into the container.  Allows piping into and out of the container as if it was another command in a shell pipeline.

Building may require privileges unless `--fake-root` is used.  Unclear what the sharp edges are there.

## Colima
Containers in Lima (Containers in Linux on Mac).  Works on MacOS, either with Intel or M1 CPUs.

[Github](https://github.com/abiosoft/colima).

Can function with Kubernetes.

## Kind
Kubernetes in Docker.

## BuildKit
Replacement for Docker for building and running images faster than Docker itself.  Baked into Docker Desktop.

# Build Environments

## Buildah
Builds images and is Linux only.
