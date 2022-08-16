Tags: #docker #podman #containers 

A Docker/Podman image's `ENTRYPOINT` runs when a container is created from it.  This can be overridden on the command line so that a different command temporarily acts as the entrypoint.

Run a shell instead of the previous `ENTRYPOINT`:
```shell
$ podman run --rm -it --entrypoint /bin/bash ubuntu/hirsute
```