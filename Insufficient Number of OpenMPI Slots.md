Tags: #scientific-computing 

OpenMPI may not properly detect the number of cores on a given system and complain about not enough slots to fulfill an application's launch (it does not oversubscribe by default):
```shell
$ mpirun -np 10 /path/to/mpi_application
There are not enough slots available in the system to satisfy the 10 slots that were requested by the application:

   /path/to/mpi_application

Either request fewer slots for your application, or make more slots available for use.

...
```

Specifying a larger number of job slots can be [[#Job Hostfile|per-job]] or [[#Default Hostfile|site-wide]].

# Hostfile Syntax
Text file with one line per node.  The number of cores per node is specified via the `slot=N` attribute:
```
host1 slots=16
host2 slots=4
host3 slots=10
```

Mapping ranks to slots is governed by the MPI application launch, but is typically in the order specified by the hostfile.

## Default Hostfile
Update `${MPI_ROOT}/etc/openmpi-default-hostfile`.

## Job Hostfile
Specify a per-job hostfile via `--hostfile /path/to/hostfile` to the MPI application launch.