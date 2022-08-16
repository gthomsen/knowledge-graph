Tags: #linux #containers #debugging 

Processes launched in a container exist on the host, though in different namespaces so as to isolate them.  The container cannot see the host and gets a different view of the world (e.g. processes have a different PID than on the host), while the host can see all of the containerized processes with their true characteristics.

Debugging within a container uses the containers characteristics while debugging a container's process from the host uses the true characteristics.  Unfortunately, neither are as easy as writing the previous statement.  Debugging within containers requires launching them with the `SYS_PTRACE` capability (via `--cap-add=SYS_PTRACE`).  Accessing a container's process requires entering into its namespaces which is a privileged process:

```shell
$ sudo nsenter --target ${HOST_PID} gdb -p ${HOST_PID}
```