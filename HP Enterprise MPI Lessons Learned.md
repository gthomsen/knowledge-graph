Tags: #mpi #fortran #scientific-computing #software-engineering 

[HP Enterprise MPI User Guide](https://support.hpe.com/hpesc/public/docDisplay?docId=a00105727en_us&docLocale=en_US) provides guidance on using HPE MPI 1.7 and Message Passing Toolkit (MPT) 2.23.

Useful tidbits:
- Fortran 2008 support via the `mpi_f08` module is only available for ifort.  Compile with `mpif08 -f08=ifort ...`
- Fortran 90 support via `mpi` is available for the Cray compiler (not 100% sure) via `mpif90 -f90=crayftn`
- FORTRAN77 support via `include mpif.h` via `mpif90 -f90=<compiler>`
- Support for threaded MPI calls without restrictions (`MPI_THREAD_MULTIPLE`) requires linking of `libmp_mt.so` and is done via the `-mt` flag on the compile wrapper
- The wrapped command line is available via `mpif90 -show ...` or `mpif08 -show`.