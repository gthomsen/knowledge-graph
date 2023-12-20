Tags: #mpi #utilities #fortran #scientific-computing 

Compiling an MPI application is typically done via a MPI distribution's compiler wrappers (e.g. `mpicc`, `mpif90`, etc) which augments the compilation options to provide whatever is necessary for MPI support (e.g. adding additional include paths for compilation, adding additional library paths and libraries for linking).

| Distribution | Option | Example |
| --- | --- | --- |
| OpenMPI | `--showme`| `mpif90 --showme -c foo.f90 -o foo.o` |
| HPE Message Passing Toolkit (MPT) | `-show` | `mpif90 -show -c foo.f90 -o foo.o` |
| Cray MPICH | `-craype-verbose` | `ftn -craype-verbose -c foo.f90 -o foo.o` |