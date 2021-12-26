Tags: #macos #docker

# Container Execution as QEMU VM
Native ARM-based containers can run as normal, though x86-64-based containers must be emulated when run on M1 hardware.  x86-64 containers will be emulated (for the most part?) though print the following warning message without additional configuration:

```shell
WARNING: The requested image's platform (linux/amd64) does not match the detected host platform (linux/arm64/v8) and no specific platform was requested
```

The above goes away by adding the `--platform linux/amd64` option:
```shell
$ docker run --platform linux/amd64 ubuntu:latest /bin/sh
#
```

Specifying a platform matters more when _building_ new images.  Without it, builds may (will?) typically fail as dependencies won't be compatible with the ARM-architecture.  This is either because the dependency can't build or doesn't have an ARM container.

Example build:
```shell
$ docker build --platform linux/arm64 -t image-name:tag .
```
