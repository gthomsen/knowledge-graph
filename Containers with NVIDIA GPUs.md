Tags: #linux #containers 

This [page](https://hackmd.io/@linnil1/BJ2OQ8crv) is surprisingly helpful.

# Debugging Podman
Run-time logging verbosity can be set via the `--log-level=debug` option:
```shell
$ podman run --log-level=debug -it --rm nvidia/cuda:11.0-base nvidia-smi
INFO[0000] podman filtering at log level debug
DEBU[0000] Called run.PersistentPreRunE(podman run --log-level=debug -it --rm --runtime nvidia nvidia/cuda:11.0-base nvidia-smi)
DEBU[0000] overlay storage already configured with a mount-program
DEBU[0000] Merged system config "/usr/share/containers/containers.conf"
DEBU[0000] overlay storage already configured with a mount-program
DEBU[0000] Using conmon: "/usr/libexec/podman/conmon"
...
```

# Configuring Podman
`/usr/share/containers/containers.conf` needs the `nvidia` run-time added to the engines list:

```
[engine.runtimes]
runc = [
...
]

# add this:
nvidia = ["/usr/bin/nvidia-container-runtime"]
```

The [[#NVIDIA Container Runtime|NVIDIA container runtime]] needs to disable `cgroups` so that containers can run without elevated privileges.  Set the following in `/etc/nvidia-container-runtime/config.toml`:
```
[nvidia-container-cli]
no-cgroups = true
```

An OCI hook to load the NVIDIA container runtime is needed.  Add the following to `/usr/share/containers/oci/hooks.d/oci-nvidia-hook.json`:

```json
{
    "version": "1.0.0",
    "hook": {
        "path": "/usr/bin/nvidia-container-toolkit",
        "args": ["nvidia-container-toolkit", "prestart"],
        "env": [
            "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
        ]
    },
    "when": {
        "always": true,
        "commands": [".*"]
    },
    "stages": ["prestart"]
}
```

Dissecting the above:
- The `hook.env` configuration specifies environment variables to inject into the container's environment.  Updating `PATH` is required so that things like `nvidia-smi` do not require full paths.
- 
## Default GPU Ownership
```shell
```

## GPUs Owned by non-root Groups
Host GPUs owned by `root:video` (or the equivalent) apparently cannot be passed through to the container with the `runc` OCI runtime, though the `crun` OCI runtime will.  See [here for details](https://github.com/containers/podman/issues/10166#issuecomment-828667904).

```shell
```


## References
- Lead on why GPUs owned by `root:video` behave differently.

# NVIDIA Container Runtime
`/etc/nvidia-container-runtime/config.toml` is the `nvidia-container-runtime`'s configuration file.

## Runtime Environment Variables
Several environment variables are parsed by `nvidia-container-runtime` and affect its behavior (e.g. maps `/usr/bin/nvidia-smi` into the container).  These can either be baked into the container image at build time (by the appropriate `ENV ...` command) or on the command line when launching the container (i.e. `-e NVIDIA_DRIVER_CAPABILITIES="compute,utility"`).

Without these, containers must provide their on installation of CUDA and the appropriate devices and libraries.

See the [NVIDIA Container Toolkit documentation](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/user-guide.html) for details.

## Debug Files
**NOTE:** These should only be set when the run-time is executing with privileges, unless one specifies an unprivileged location.

There are two log files that can be specified for logging debug information.  
```
[nvidia-container-cli]
debug = "/var/log/nvidia-container-toolkit.log"
...

[nvidia-container-runtime]
debug = "/var/log/nvidia-container-runtime.log"
...
```


## Listing Mapped Files
List the files that will be bind mounted into the containers via the OCI runtime hooks:
```shell
$ nvidia-container-cli -k list | xargs ls -la
crw-rw---- 1 root                vglusers             195,   0 Aug  1  2021 /dev/nvidia0
crw-rw---- 1 root                vglusers             195, 255 Aug  1  2021 /dev/nvidiactl
crw-rw---- 1 root                vglusers             195, 254 Aug  1  2021 /dev/nvidia-modeset
crw-rw-rw- 1 root                root                 234,   0 Aug  1  2021 /dev/nvidia-uvm
crw-rw-rw- 1 root                root                 234,   1 Aug  1  2021 /dev/nvidia-uvm-tools
srwxrwxrwx 1 nvidia-persistenced nvidia-persistenced         0 Aug  1  2021 /run/nvidia-persistenced/socket
-rwxr-xr-x 1 root                root                    45888 Jul  2  2021 /usr/bin/nvidia-cuda-mps-control
-rwxr-xr-x 1 root                root                    14488 Jul  2  2021 /usr/bin/nvidia-cuda-mps-server
-rwxr-xr-x 1 root                root                   248624 Jul  2  2021 /usr/bin/nvidia-debugdump
-rwxr-xr-x 1 root                root                   208336 Jul  2  2021 /usr/bin/nvidia-persistenced
-rwxr-xr-x 1 root                root                   653368 Jul  2  2021 /usr/bin/nvidia-smi
-rw-r--r-- 1 root                root                 20385228 Jul  2  2021 /usr/lib/i386-linux-gnu/libcuda.so.460.91.03
...
```