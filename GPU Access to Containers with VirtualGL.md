Tags: #docker #gpu 

**NOTE:** This is incomplete and is provided to document what was done on a previous server setup.

Seeing the following error message when launching a container using `nvidia-docker` indicates the current user does not have access to the GPU:
```shell
Failed to initialize NVML: Insufficient Permissions
```

For VirtualGL-based setups, this requires adding `root:vglusers` into `/etc/nvidia-container-runtime/config.yml`.  Then the following should work:
```shell
$ nvidia-docker run --privileged -v`pwd`:/workspace/host --rm -it --name pytorch nvcr.io/nvidia/pytorch:21.04-py3
```

Derived from this Stack Overflow [post](https://stackoverflow.com/questions/52507744/enable-nvidia-smi-permissions-to-be-run-by-all-users).