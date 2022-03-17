Tags: #containers #podman #singularity

As of 2022/03/14 it is not possible to directly interact with a local Podman registry.  This forces export of the layers to disk so that Singuarlity can access it via the `docker-archive://` protocol.

**NOTE:** This is inefficient as the Podman image is read and written to disk.  Be mindful of working with large (i.e. multi-GiB) images as you'll both need at least 3x the diskspace (Podman original, Podman export, Singularity export) and time spent waiting for I/O.

```shell
$ podman images
REPOSITORY                TAG      IMAGE ID      CREATED      SIZE
localhost/ifort-classic   latest   7b290187ed88  2 days ago   7.52 GB

$ podman save -o ifort-classic-export.tar ifort-classic.latest

$ singularity build ifort-classic.sif docker-archive://ifort-classic-export.tar
```
