Tags: #linux #utilities 

Shells typically provide `ulimit` to modify its, and any processes spawned, resource limits.  Unfortunately, non-privileged shells do not allow limits to be raised - either from their default, or from a lowered value.  This requires adjusting the limit via `prlimit` (in the `util-linux` package on Ubuntu 22.04).

Removing the maximum stack size for a given process:
```shell
$ sudo prlimit -s=unlimited -p <pid>
```

***NOTE:*** All of the resource options require an equal sign between the option and the new value.  It is not optional!