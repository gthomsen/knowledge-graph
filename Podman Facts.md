Tags: #containers 

Random collection of Podman facts.

# Privileged Containers
Podman runs containers unprivileged by default.  This translates to roughly:
- Explicitly dropping capabilities
- Limiting the devices mapped into the container
- Mapping read-only volumes
- MAC via Apparmor/SELinux
- Enabling Seccomp filters

Specifying the `--privileged` flag does not enable the above which allows the container to run with the same privileges as the user launching.

# Using Docker's Registry
`docker.io` is the registry name that resolves to `hub.docker.com`. 

```shell
$ podman pull docker.io/library/postgres
```